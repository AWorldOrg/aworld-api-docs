## Quiz API

[Back to Index](./../README.md)

Questa sezione descrive gli endpoint REST API per la gestione dei quiz.

### Get Quiz

Recupera i dettagli di un quiz specifico.

#### Request

```http
GET /api/v1/quiz/{id}
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| id        | string | Yes      | Identificatore del quiz        |
| lang      | string | No       | Codice lingua (es. 'it', 'en') |

#### Response

```json
{
  "data": {
    "id": "string",
    "difficultyLevel": "easy|medium|hard",
    "potentialRewards": [
      {
        "kind": "string",
        "amount": number
      }
    ],
    "document": {
      "explanation": "string",
      "correctAnswer": "string",
      "opt1": "string",
      "opt2": "string",
      "opt3": "string",
      "opt4": "string",
      "question": "string"
    },
    "sdg": "string",
    "topic": "string",
    "category": "string",
    "log": {
      "outcome": "success|fail",
      "difficultyLevel": "easy|medium|hard",
      "updatedAt": "string"
    }
  }
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Restituisce i dettagli del quiz     |
| 400         | Bad Request - Parametri mancanti o non validi |
| 404         | Not Found - Quiz non trovato                  |
| 500         | Internal Server Error - Errore del server     |

### Get Random Quiz

Recupera un quiz casuale con un determinato livello di difficoltà.

#### Request

```http
GET /api/v1/quiz/random
```

#### Query Parameters

| Parameter       | Type   | Required | Description                                |
| --------------- | ------ | -------- | ------------------------------------------ |
| difficultyLevel | string | Yes      | Livello di difficoltà (easy, medium, hard) |
| lang            | string | No       | Codice lingua (es. 'it', 'en')             |

#### Response

```json
{
  "data": {
    "id": "string",
    "difficultyLevel": "easy|medium|hard",
    "potentialRewards": [
      {
        "kind": "string",
        "amount": number
      }
    ],
    "document": {
      "explanation": "string",
      "correctAnswer": "string",
      "opt1": "string",
      "opt2": "string",
      "opt3": "string",
      "opt4": "string",
      "question": "string"
    }
  }
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Restituisce un quiz casuale         |
| 400         | Bad Request - Parametri mancanti o non validi |
| 404         | Not Found - Nessun quiz disponibile           |
| 500         | Internal Server Error - Errore del server     |

### Submit Quiz Answer

Invia la risposta a un quiz.

#### Request

```http
POST /api/v1/quiz/{id}/submit
```

#### Request Body

```json
{
  "answer": "string"
}
```

#### Response

```json
{
  "data": {
    "id": "string",
    "difficultyLevel": "easy|medium|hard",
    "outcome": "success|fail",
    "document": {
      "explanation": "string",
      "correctAnswer": "string"
    },
    "log": {
      "outcome": "success|fail",
      "updatedAt": "string"
    }
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

- I livelli di difficoltà disponibili sono: "easy", "medium", "hard"
- L'outcome può essere: "success" o "fail"
- Il campo `explanation` viene fornito solo dopo aver sottomesso una risposta
- I `potentialRewards` indicano i premi ottenibili completando il quiz
- Il campo `log` contiene lo storico delle risposte dell'utente per quel quiz
- Le risposte sono case-sensitive e devono corrispondere esattamente a una delle opzioni fornite
