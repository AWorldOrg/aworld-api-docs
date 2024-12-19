## Missions API

[Back to Index](./README.md)

Questa sezione descrive gli endpoint REST API per la gestione delle missioni.

### List Missions

Recupera l'elenco delle missioni disponibili per l'utente.

#### Request

```http
GET /v1/missions
```

#### Query Parameters

| Parameter | Type   | Required | Description                              |
| --------- | ------ | -------- | ---------------------------------------- |
| lang      | string | Yes      | Codice lingua (es. 'it', 'en')           |
| teamId    | string | No       | ID del team per filtrare le missioni     |
| projectId | string | No       | ID del progetto per filtrare le missioni |
| timezone  | string | No       | Timezone dell'utente (es. 'Europe/Rome') |

#### Response

```json
{
  "data": [
    {
      "id": "string",
      "projectId": "string",
      "teamId": "string",
      "missionCatalogId": "string",
      "type": "episode|action|quiz|mobility|activity|streak|exp",
      "specialType": "onboarding",
      "timeframe": "DAILY|WEEKLY|MONTHLY",
      "difficultyLevel": "easy|medium|hard|champion",
      "target": 0,
      "count": 0,
      "completed": false,
      "image": "string",
      "document": {
        "title": "string",
        "body": [
          {
            "sliceType": "string",
            // Altri campi del body slice in base al tipo
          }
        ]
      },
      "createdAt": "2024-01-01T00:00:00Z",
      "updatedAt": "2024-01-01T00:00:00Z",
      "potentialRewards": [
        {
          "kind": "string",
          "min": 0,
          "max": 0
        }
      ],
      "rewards": [
        {
          "id": "string",
          "kind": "string", 
          "status": "TO_REDEEM|COMPLETED",
          "amount": 0,
          "createdAt": "2024-01-01T00:00:00Z",
          "updatedAt": "2024-01-01T00:00:00Z"
        }
      ]
    }
  ]
}
```

#### Status Codes

| Status Code | Description                                                       |
| ----------- | ----------------------------------------------------------------- |
| 200         | Success - Restituisce l'elenco delle missioni                     |
| 400         | Bad Request - Parametri mancanti o non validi                     |
| 401         | Unauthorized - Token di autenticazione mancante o non valido      |
| 403         | Forbidden - L'utente non ha i permessi per accedere alle missioni |
| 500         | Internal Server Error - Errore del server                         |

#### Note

- Le missioni sono filtrate in base ai permessi dell'utente autenticato
- Il campo `specialType` è presente solo per missioni speciali (es. onboarding)
- I `potentialRewards` indicano i possibili premi che l'utente può ottenere completando la missione
- I `rewards` mostrano i premi effettivamente ottenuti dall'utente per quella missione
