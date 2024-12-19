## Community Missions API

[Back to Index](./README.md)

Questa sezione descrive gli endpoint REST API per la gestione delle missioni comunitarie.

### Get Community Mission

Recupera i dettagli di una missione comunitaria specifica.

#### Request

```http
GET /api/v1/community-mission/{id}
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| id        | string | Yes      | Identificatore della missione  |
| lang      | string | No       | Codice lingua (es. 'it', 'en') |

#### Response

```json
{
  "data": {
    "id": "string",
    "type": "communityMission",
    "attributes": {
      "name": "string",
      "startsAt": "string",
      "endsAt": "string",
      "targetAmount": number,
      "currentAmount": number,
      "userCount": number,
      "isJoined": boolean
    }
  }
}
```

#### Status Codes

| Status Code | Description                                     |
| ----------- | ----------------------------------------------- |
| 200         | Success - Restituisce i dettagli della missione |
| 400         | Bad Request - Parametri mancanti o non validi   |
| 404         | Not Found - Missione non trovata                |
| 500         | Internal Server Error - Errore del server       |

### List Live Community Missions

Recupera la lista delle missioni comunitarie attualmente attive.

#### Request

```http
GET /api/v1/community-missions/live
```

#### Query Parameters

| Parameter   | Type   | Required | Description                    |
| ----------- | ------ | -------- | ------------------------------ |
| lang        | string | No       | Codice lingua (es. 'it', 'en') |
| communityId | string | No       | Filtra per comunità specifica  |

#### Response

```json
{
  "data": {
    "items": [
      {
        "id": "string",
        "type": "communityMission",
        "attributes": {
          "name": "string",
          "startsAt": "string",
          "endsAt": "string"
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
| 200         | Success - Restituisce la lista delle missioni attive |
| 400         | Bad Request - Parametri non validi                   |
| 500         | Internal Server Error - Errore del server            |

### Join Community Mission

Partecipa a una missione comunitaria.

#### Request

```http
POST /api/v1/community-missions/{id}/join
```

#### Response

```json
{
  "data": {
    "communityMissionId": "string",
    "userId": "string",
    "joinedAt": "string"
  }
}
```

#### Status Codes

| Status Code | Description                                      |
| ----------- | ------------------------------------------------ |
| 200         | Success - Partecipazione registrata con successo |
| 400         | Bad Request - Missione non disponibile           |
| 401         | Unauthorized - Utente non autorizzato            |
| 404         | Not Found - Missione non trovata                 |
| 500         | Internal Server Error - Errore del server        |

### Get Community Mission Leaderboard

Recupera la classifica di una missione comunitaria.

#### Request

```http
GET /api/v1/community-missions/{id}/leaderboard
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
        "rank": "string",
        "userId": "string",
        "metricSum": number,
        "user": {
          "first_name": "string",
          "last_name": "string"
        }
      }
    ],
    "userPosition": {
      "rank": "string",
      "metricSum": number
    },
    "nextToken": "string"
  }
}
```

#### Status Codes

| Status Code | Description                               |
| ----------- | ----------------------------------------- |
| 200         | Success - Restituisce la classifica       |
| 400         | Bad Request - Parametri non validi        |
| 404         | Not Found - Missione non trovata          |
| 500         | Internal Server Error - Errore del server |

### List User Community Missions

Recupera la lista delle missioni comunitarie dell'utente.

#### Request

```http
GET /api/v1/community-missions/user
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| lang      | string | No       | Codice lingua (es. 'it', 'en') |

#### Response

```json
{
  "data": {
    "items": [
      {
        "communityMissionId": "string",
        "communityMission": {
          "name": "string",
          "type": "string"
        },
        "joinedAt": "string",
        "targetReached": "string"
      }
    ]
  }
}
```

#### Status Codes

| Status Code | Description                                               |
| ----------- | --------------------------------------------------------- |
| 200         | Success - Restituisce la lista delle missioni dell'utente |
| 401         | Unauthorized - Utente non autorizzato                     |
| 500         | Internal Server Error - Errore del server                 |

#### Note

- Le missioni sono considerate "live" solo se la data corrente è compresa tra `startsAt` e `endsAt`
- Il campo `targetReached` indica quando l'utente ha raggiunto l'obiettivo della missione
- La classifica è ordinata per `metricSum` in ordine decrescente
- `userPosition` mostra la posizione dell'utente corrente nella classifica
