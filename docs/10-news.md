## News API

[Back to Index](./../README.md)

Questa sezione descrive gli endpoint REST API per la gestione delle news.

### Get News

Recupera i dettagli di una news specifica.

#### Request

```http
GET /api/v1/news/{id}
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| id        | string | Yes      | Identificatore della news      |
| lang      | string | Yes      | Codice lingua (es. 'it', 'en') |

#### Response

```json
{
  "data": {
    "id": "string",
    "teamId": "string",
    "startsAt": "string",
    "endsAt": "string",
    "sort": number,
    "document": {
      "title": "string",
      "image": "string",
      "tagline": "string",
      "redirectUrl": "string",
      "body": [
        {
          "sliceType": "string",
          // Altri campi del body slice in base al tipo
        }
      ]
    },
    "read": boolean,
    "points": number,
    "quizzes": [
      {
        "id": "string",
        "order": number,
        "status": "TODO|SUCCESS|FAILED",
        "document": {
          "question": "string",
          "opt1": "string",
          "opt2": "string",
          "opt3": "string",
          "opt4": "string",
          "correctAnswer": "string",
          "explanation": "string"
        }
      }
    ],
    "potentialRewards": [
      {
        "kind": "string",
        "amount": number
      }
    ]
  }
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Restituisce i dettagli della news   |
| 400         | Bad Request - Parametri mancanti o non validi |
| 404         | Not Found - News non trovata                  |
| 500         | Internal Server Error - Errore del server     |

### List Live News

Recupera la lista delle news attualmente attive.

#### Request

```http
GET /api/v1/news/live
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| teamId    | string | No       | Filtra per team specifico      |
| lang      | string | Yes      | Codice lingua (es. 'it', 'en') |
| limit     | number | No       | Numero di risultati per pagina |
| nextToken | string | No       | Token per la paginazione       |

#### Response

```json
{
  "data": {
    "items": [
      {
        "id": "string",
        "teamId": "string",
        "startsAt": "string",
        "endsAt": "string",
        "document": {
          "title": "string",
          "image": "string",
          "tagline": "string"
        },
        "read": boolean
      }
    ],
    "nextToken": "string"
  }
}
```

#### Status Codes

| Status Code | Description                                      |
| ----------- | ------------------------------------------------ |
| 200         | Success - Restituisce la lista delle news attive |
| 400         | Bad Request - Parametri non validi               |
| 500         | Internal Server Error - Errore del server        |

### List Past News

Recupera la lista delle news passate.

#### Request

```http
GET /api/v1/news/past
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| teamId    | string | No       | Filtra per team specifico      |
| lang      | string | Yes      | Codice lingua (es. 'it', 'en') |
| limit     | number | No       | Numero di risultati per pagina |
| nextToken | string | No       | Token per la paginazione       |

#### Response

```json
{
  "data": {
    "items": [
      {
        "id": "string",
        "teamId": "string",
        "startsAt": "string",
        "endsAt": "string",
        "document": {
          "title": "string",
          "image": "string",
          "tagline": "string"
        },
        "read": boolean
      }
    ],
    "nextToken": "string"
  }
}
```

#### Status Codes

| Status Code | Description                                       |
| ----------- | ------------------------------------------------- |
| 200         | Success - Restituisce la lista delle news passate |
| 400         | Bad Request - Parametri non validi                |
| 500         | Internal Server Error - Errore del server         |

### Submit News Quiz Answer

Invia la risposta a un quiz associato a una news.

#### Request

```http
POST /api/v1/news/quiz/{quizId}/answer
```

#### Request Body

```json
{
  "answer": "string",
  "lang": "string"
}
```

#### Response

```json
{
  "data": {
    "quizId": "string",
    "correct": boolean
  }
}
```

#### Status Codes

| Status Code | Description                                |
| ----------- | ------------------------------------------ |
| 200         | Success - Risposta registrata con successo |
| 400         | Bad Request - Risposta non valida          |
| 404         | Not Found - Quiz non trovato               |
| 500         | Internal Server Error - Errore del server  |

#### Note

- Le news sono considerate "live" se la data corrente è compresa tra `startsAt` e `endsAt`
- Il campo `read` indica se l'utente ha già letto la news
- I quiz associati hanno tre possibili stati: "TODO", "SUCCESS", "FAILED"
- Le risposte ai quiz sono verificate case-sensitive
- I `potentialRewards` indicano i premi ottenibili completando la news e i suoi quiz
- Il campo `redirectUrl` nel documento può essere utilizzato per reindirizzare a contenuti esterni
