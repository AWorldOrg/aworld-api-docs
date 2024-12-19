## Authentication API

[Back to Index](./README.md)

Questa sezione descrive i meccanismi di autenticazione e le regole comuni per tutte le API REST.

### Headers Richiesti

Tutte le richieste API devono includere gli headers di autenticazione.

#### Headers

| Header      | Required | Example   | Description                        |
| ----------- | -------- | --------- | ---------------------------------- |
| x-aw-uid    | Yes      | USER123   | Identificatore univoco dell'utente |
| x-aw-tenant | Yes      | TENANT123 | Identificatore dell'istanza Client |

#### Status Codes

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| 200         | Success - Richiesta completata con successo         |
| 400         | Bad Request - Parametri mancanti o non validi       |
| 401         | Unauthorized - Autenticazione mancante o non valida |
| 403         | Forbidden - L'utente non ha i permessi necessari    |
| 404         | Not Found - Risorsa non trovata                     |
| 429         | Too Many Requests - Superato il limite di richieste |
| 500         | Internal Server Error - Errore del server           |

### Rate Limiting

Il sistema implementa limiti di richieste per proteggere le API.

#### Limiti

| Tipo       | Limite         |
| ---------- | -------------- |
| Per Minuto | 100 richieste  |
| Per Ora    | 1000 richieste |

#### Headers di Rate Limit

| Header                | Description                                        |
| --------------------- | -------------------------------------------------- |
| X-RateLimit-Limit     | Numero massimo di richieste permesse               |
| X-RateLimit-Remaining | Numero di richieste rimanenti nel periodo corrente |
| X-RateLimit-Reset     | Timestamp Unix di quando il limite verrà resettato |

### Formato Risposte

#### Esempio di Errore

```json
{
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Missing x-aw-externalId header"
  }
}
```

#### Esempio di Successo

```json
{
  "data": {
    "id": "123",
    "type": "user",
    "attributes": {
      "name": "John Doe",
      "email": "john@example.com"
    }
  }
}
```

#### Note

- Gli headers di autenticazione sono obbligatori per tutte le richieste
- L'identificatore utente deve essere valido nel sistema
- Headers mancanti risulteranno in un errore 401
- I limiti di rate sono applicati per identificatore utente
- Gli headers di rate limiting sono inclusi in tutte le risposte
- Tutte le risposte seguono un formato JSON standard
- Gli errori includono sempre un codice e un messaggio descrittivo
