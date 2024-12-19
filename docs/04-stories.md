## Stories API

[Back to Index](./../README.md)

Questa sezione descrive gli endpoint REST API per la gestione delle storie.

### Get Story

Recupera i dettagli di una storia specifica.

#### Request

```http
GET /api/v1/stories/{id}
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| id        | string | Yes      | Identificatore della storia    |
| lang      | string | Yes      | Codice lingua (es. 'it', 'en') |

#### Response

```json
{
  "data": {
    "id": "string",
    "type": "stories",
    "attributes": {
      "title": "string",
      "image": "string",
      "category": {
        "id": "string",
        "name": "string"
      },
      "favorited": boolean,
      "favoritedByPeople": number
    }
  }
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Restituisce i dettagli della storia |
| 400         | Bad Request - Parametri mancanti o non validi |
| 404         | Not Found - Storia non trovata                |
| 500         | Internal Server Error - Errore del server     |

### List Stories

Recupera una lista di storie filtrata.

#### Request

```http
GET /api/v1/stories
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| lang      | string | Yes      | Codice lingua (es. 'it', 'en') |
| text      | string | No       | Testo da cercare               |
| category  | string | No       | Filtra per categoria           |
| topic     | string | No       | Filtra per topic               |
| sdg       | string | No       | Filtra per SDG                 |
| sdgTarget | string | No       | Filtra per target SDG          |
| limit     | number | No       | Numero di risultati per pagina |
| nextToken | string | No       | Token per la paginazione       |

#### Response

```json
{
  "data": {
    "items": [
      {
        "id": "string",
        "type": "stories",
        "attributes": {
          "title": "string",
          "image": "string"
        }
      }
    ],
    "nextToken": "string"
  }
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Restituisce la lista delle storie   |
| 400         | Bad Request - Parametri mancanti o non validi |
| 500         | Internal Server Error - Errore del server     |

### Submit Progress

Registra il progresso dell'utente in una storia.

#### Request

```http
POST /api/v1/stories/progress
```

#### Request Body

```json
{
  "journeyId": "string",
  "episodeId": "string",
  "slideId": "string",
  "slideType": "string",
  "lang": "string",
  "engageTime": number
}
```

#### Response

```json
{
  "data": {
    "progression": {
      "id": "string",
      "episodeId": "string",
      "completed": boolean,
      "engageTime": number
    },
    "episodeCompleted": boolean,
    "journeyCompleted": boolean
  }
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Progresso registrato con successo   |
| 400         | Bad Request - Parametri mancanti o non validi |
| 401         | Unauthorized - Utente non autorizzato         |
| 500         | Internal Server Error - Errore del server     |

### Submit Feedback

Invia un feedback per una storia.

#### Request

```http
POST /api/v1/stories/{id}/feedback
```

#### Request Body

```json
{
  "rating": "LIKE|DISLIKE"
}
```

#### Response

```json
{
  "data": {
    "id": "string",
    "type": "stories",
    "attributes": {
      "feedback": "string",
      "updatedAt": "string"
    }
  }
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Feedback registrato con successo    |
| 400         | Bad Request - Parametri mancanti o non validi |
| 404         | Not Found - Storia non trovata                |
| 500         | Internal Server Error - Errore del server     |

### Get Popular Stories

Recupera le storie più popolari.

#### Request

```http
GET /api/v1/stories/popular
```

#### Query Parameters

| Parameter        | Type   | Required | Description                             |
| ---------------- | ------ | -------- | --------------------------------------- |
| lang             | string | Yes      | Codice lingua (es. 'it', 'en')          |
| pastPeriodInDays | number | No       | Periodo per il calcolo della popolarità |
| limit            | number | No       | Numero di risultati per pagina          |
| nextToken        | string | No       | Token per la paginazione                |

#### Response

```json
{
  "data": {
    "items": [
      {
        "id": "string",
        "type": "stories",
        "attributes": {
          "title": "string",
          "image": "string",
          "favoritedByPeople": number
        }
      }
    ],
    "nextToken": "string"
  }
}
```

#### Status Codes

| Status Code | Description                                          |
| ----------- | ---------------------------------------------------- |
| 200         | Success - Restituisce la lista delle storie popolari |
| 400         | Bad Request - Parametri mancanti o non validi        |
| 500         | Internal Server Error - Errore del server            |

#### Note

- Il rating può essere solo "LIKE" o "DISLIKE"
- Il campo `favoritedByPeople` indica il numero totale di utenti che hanno messo mi piace
- La popolarità è calcolata in base al numero di mi piace nel periodo specificato
- Se `pastPeriodInDays` non è specificato, viene utilizzato un periodo predefinito
