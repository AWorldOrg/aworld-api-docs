## Calendar API

[Back to Index](./README.md)

Questa sezione descrive gli endpoint REST API per la gestione del calendario e delle attività giornaliere.

### Get Daily Calendar

Recupera le attività per un giorno specifico.

#### Request

```http
GET /api/v1/calendar/daily
```

#### Query Parameters

| Parameter | Type   | Required | Description                              |
| --------- | ------ | -------- | ---------------------------------------- |
| date      | string | Yes      | Data nel formato YYYY-MM-DD              |
| projectId | string | No       | ID del progetto                          |
| timezone  | string | No       | Timezone dell'utente (es. 'Europe/Rome') |

#### Response

```json
{
  "data": {
    "date": "string",
    "projectId": "string",
    "activities": [
      {
        "id": "string",
        "sourceId": "string",
        "sourceKind": "episode|action|quiz|mobility|news|footprint|survey",
        "sourceLogId": "string",
        "sourceLogKind": "string",
        "createdAt": "string",
        "updatedAt": "string"
      }
    ]
  }
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Restituisce le attività del giorno  |
| 400         | Bad Request - Parametri mancanti o non validi |
| 500         | Internal Server Error - Errore del server     |

### Get Calendar Preview

Recupera una panoramica del calendario con streak e attività.

#### Request

```http
GET /api/v1/calendar/preview
```

#### Query Parameters

| Parameter | Type   | Required | Description                              |
| --------- | ------ | -------- | ---------------------------------------- |
| fromDate  | string | Yes      | Data iniziale (YYYY-MM-DD)               |
| toDate    | string | No       | Data finale (YYYY-MM-DD)                 |
| projectId | string | No       | ID del progetto                          |
| timezone  | string | No       | Timezone dell'utente (es. 'Europe/Rome') |
| userId    | string | No       | ID utente (per admin)                    |

#### Response

```json
{
  "data": {
    "months": [
      {
        "month": "string",
        "projectId": "string",
        "userId": "string",
        "streak": [
          {
            "projectId": "string",
            "iterationId": number,
            "kind": "REGULAR|FREEZE",
            "count": number
          }
        ]
      }
    ],
    "weeks": [
      {
        "week": "string",
        "projectId": "string",
        "fromDate": "string",
        "toDate": "string",
        "userId": "string",
        "streak": [
          {
            "projectId": "string",
            "iterationId": number,
            "kind": "REGULAR|FREEZE",
            "count": number,
            "perfect": boolean
          }
        ]
      }
    ],
    "days": [
      {
        "date": "string",
        "projectId": "string",
        "userId": "string",
        "activities": boolean,
        "exp": number,
        "streak": {
          "regular": boolean,
          "freeze": boolean
        }
      }
    ]
  }
}
```

#### Status Codes

| Status Code | Description                                     |
| ----------- | ----------------------------------------------- |
| 200         | Success - Restituisce la preview del calendario |
| 400         | Bad Request - Parametri mancanti o non validi   |
| 500         | Internal Server Error - Errore del server       |

### Get Monthly Streak

Recupera le informazioni sulle streak per un mese specifico.

#### Request

```http
GET /api/v1/calendar/streak/monthly
```

#### Query Parameters

| Parameter | Type   | Required | Description              |
| --------- | ------ | -------- | ------------------------ |
| month     | string | Yes      | Mese nel formato YYYY-MM |
| projectId | string | No       | ID del progetto          |

#### Response

```json
{
  "data": [
    {
      "projectId": "string",
      "iterationId": number,
      "kind": "REGULAR|FREEZE",
      "count": number
    }
  ]
}
```

#### Status Codes

| Status Code | Description                                   |
| ----------- | --------------------------------------------- |
| 200         | Success - Restituisce le streak del mese      |
| 400         | Bad Request - Parametri mancanti o non validi |
| 500         | Internal Server Error - Errore del server     |

#### Note

- Le attività possono essere di vari tipi: episode, action, quiz, mobility, news, footprint, survey
- Le streak possono essere di due tipi: REGULAR (normali) o FREEZE (congelate)
- Una streak "perfect" indica che tutte le attività richieste sono state completate
- Il campo `activities` nei giorni indica se ci sono attività completate in quella data
- Il campo `exp` indica i punti esperienza guadagnati in quel giorno
- La preview del calendario include viste per mesi, settimane e giorni
- Le date devono essere nel formato YYYY-MM-DD
- Il timezone è importante per il corretto calcolo delle streak giornaliere
