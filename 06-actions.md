## Actions API

[Back to Index](./README.md)

Questa sezione descrive gli endpoint REST API per la gestione delle azioni.

### Get Action

Recupera i dettagli di un'azione specifica.

#### Request

```http
GET /api/v1/actions/{id}
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| id        | string | Yes      | Identificatore dell'azione     |
| location  | object | Yes      | Oggetto location con type e id |
| lang      | string | Yes      | Codice lingua (es. 'it', 'en') |

#### Response

```json
{
  "data": {
    "id": "string",
    "type": "action",
    "attributes": {
      "handle": "string",
      "image": "string",
      "dailyCounter": number,
      "timesPerDay": number,
      "isRepeatable": boolean
    }
  }
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Restituisce i dettagli dell'azione  |
| 400         | Bad Request - Parametri mancanti o non validi |
| 404         | Not Found - Azione non trovata                |
| 500         | Internal Server Error - Errore del server     |

### List Actions

Recupera una lista di azioni filtrata.

#### Request

```http
GET /api/v1/actions
```

#### Query Parameters

| Parameter  | Type   | Required | Description                    |
| ---------- | ------ | -------- | ------------------------------ |
| categoryId | string | No       | Filtra per categoria           |
| teamId     | string | No       | Filtra per team                |
| location   | object | Yes      | Oggetto location con type e id |
| lang       | string | Yes      | Codice lingua (es. 'it', 'en') |
| limit      | number | No       | Numero di risultati per pagina |
| nextToken  | string | No       | Token per la paginazione       |

#### Response

```json
{
  "data": {
    "items": [
      {
        "id": "string",
        "type": "action",
        "attributes": {
          "handle": "string",
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
| 200         | Success - Restituisce la lista delle azioni   |
| 400         | Bad Request - Parametri mancanti o non validi |
| 500         | Internal Server Error - Errore del server     |

### Submit Action

Sottomette una o più azioni completate dall'utente.

#### Request

```http
POST /api/v1/actions/submit
```

#### Request Body

```json
{
  "projectId": "string",
  "teamId": "string",
  "actions": [
    {
      "id": "string"
    }
  ],
  "location": {
    "type": "string",
    "id": "string"
  },
  "timezone": "string",
  "lang": "string"
}
```

#### Response

```json
{
  "data": {
    "actionLogs": [
      {
        "id": "string",
        "actionId": "string",
        "timestamp": "string"
      }
    ]
  }
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Azioni sottomesse con successo      |
| 400         | Bad Request - Parametri mancanti o non validi |
| 401         | Unauthorized - Utente non autorizzato         |
| 500         | Internal Server Error - Errore del server     |

### Search Actions

Cerca azioni in base a criteri specifici.

#### Request

```http
GET /api/v1/actions/search
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| text      | string | No       | Testo da cercare               |
| category  | string | No       | Filtra per categoria           |
| sdg       | string | No       | Filtra per SDG                 |
| location  | object | Yes      | Oggetto location con type e id |
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
        "type": "action",
        "attributes": {
          "handle": "string",
          "image": "string"
        }
      }
    ],
    "total": number,
    "nextToken": "string"
  }
}
```

#### Status Codes

| Status Code | Description                                     |
| ----------- | ----------------------------------------------- |
| 200         | Success - Restituisce i risultati della ricerca |
| 400         | Bad Request - Parametri mancanti o non validi   |
| 500         | Internal Server Error - Errore del server       |

#### Note

- La ricerca è case-insensitive
- Il campo `total` indica il numero totale di risultati disponibili
- I risultati sono ordinati per rilevanza
- La paginazione è gestita tramite `limit` e `nextToken`
