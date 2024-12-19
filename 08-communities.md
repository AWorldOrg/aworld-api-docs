## Communities API

[Back to Index](./README.md)

Questa sezione descrive gli endpoint REST API per la gestione delle comunità.

### Get Community

Recupera i dettagli di una comunità specifica.

#### Request

```http
GET /api/v1/communities/{id}
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| id        | string | Yes      | Identificatore della comunità  |
| lang      | string | No       | Codice lingua (es. 'it', 'en') |
| location  | object | No       | Oggetto location con type e id |

#### Response

```json
{
  "data": {
    "id": "string",
    "type": "community",
    "attributes": {
      "name": "string",
      "stage": "string",
      "isPremium": boolean,
      "accessType": "string",
      "userCount": number,
      "isJoined": boolean,
      "groups": [],
      "metrics": [],
      "document": {
        "title": "string",
        "logo": "string"
      }
    }
  }
}
```

#### Status Codes

| Status Code | Description                                     |
| ----------- | ----------------------------------------------- |
| 200         | Success - Restituisce i dettagli della comunità |
| 400         | Bad Request - Parametri mancanti o non validi   |
| 404         | Not Found - Comunità non trovata                |
| 500         | Internal Server Error - Errore del server       |

### List Communities

Recupera la lista delle comunità disponibili.

#### Request

```http
GET /api/v1/communities
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| lang      | string | No       | Codice lingua (es. 'it', 'en') |
| location  | object | No       | Oggetto location con type e id |
| limit     | number | No       | Numero di risultati per pagina |
| nextToken | string | No       | Token per la paginazione       |

#### Response

```json
{
  "data": {
    "items": [
      {
        "id": "string",
        "type": "community",
        "attributes": {
          "name": "string",
          "stage": "string",
          "userCount": number,
          "document": {
            "title": "string",
            "logo": "string"
          }
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
| 200         | Success - Restituisce la lista delle comunità |
| 400         | Bad Request - Parametri non validi            |
| 500         | Internal Server Error - Errore del server     |

### Join Community

Partecipa a una comunità.

#### Request

```http
POST /api/v1/communities/{id}/join
```

#### Request Body

```json
{
  "activationCode": "string",
  "location": {
    "type": "string",
    "id": "string"
  }
}
```

#### Response

```json
{
  "data": {
    "teamId": "string",
    "userId": "string",
    "isAdmin": boolean,
    "isPrimary": boolean
  }
}
```

#### Status Codes

| Status Code | Description                                      |
| ----------- | ------------------------------------------------ |
| 200         | Success - Partecipazione registrata con successo |
| 400         | Bad Request - Codice di attivazione non valido   |
| 401         | Unauthorized - Utente non autorizzato            |
| 404         | Not Found - Comunità non trovata                 |
| 500         | Internal Server Error - Errore del server        |

### List Community Members

Recupera la lista dei membri di una comunità.

#### Request

```http
GET /api/v1/communities/{id}/members
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| limit     | number | No       | Numero di risultati per pagina |
| nextToken | string | No       | Token per la paginazione       |

#### Response

```json
{
  "data": {
    "items": [
      {
        "userId": "string",
        "teamId": "string",
        "isAdmin": boolean,
        "user": {
          "first_name": "string",
          "last_name": "string"
        }
      }
    ],
    "nextToken": "string"
  }
}
```

#### Status Codes

| Status Code | Description                               |
| ----------- | ----------------------------------------- |
| 200         | Success - Restituisce la lista dei membri |
| 400         | Bad Request - Parametri non validi        |
| 404         | Not Found - Comunità non trovata          |
| 500         | Internal Server Error - Errore del server |

### List Community Groups

Recupera la lista dei gruppi di una comunità.

#### Request

```http
GET /api/v1/communities/{id}/groups
```

#### Response

```json
{
  "data": {
    "items": [
      {
        "groupId": "string",
        "name": "string",
        "userCount": number
      }
    ]
  }
}
```

#### Status Codes

| Status Code | Description                               |
| ----------- | ----------------------------------------- |
| 200         | Success - Restituisce la lista dei gruppi |
| 404         | Not Found - Comunità non trovata          |
| 500         | Internal Server Error - Errore del server |

#### Note

- Il campo `stage` può essere: "live", "hidden", "featured"
- Il campo `accessType` può essere: "public", "activationCode", "sso"
- L'`activationCode` è richiesto solo per comunità con `accessType` = "activationCode"
- Gli amministratori (`isAdmin` = true) hanno accesso a funzionalità aggiuntive
- Il campo `isPrimary` indica se la comunità è quella principale dell'utente
