## Users API

[Back to Index](./README.md)

Questa sezione descrive gli endpoint REST API per la gestione degli utenti.

### Get User Profile

Recupera il profilo dell'utente autenticato.

#### Request

```http
GET /api/v1/user
```

#### Query Parameters

| Parameter | Type   | Required | Description                    |
| --------- | ------ | -------- | ------------------------------ |
| lang      | string | No       | Codice lingua (es. 'it', 'en') |

#### Response

```json
{
  "data": {
    "userId": "string",
    "type": "user",
    "attributes": {
      "first_name": "string",
      "last_name": "string",
      "email": "string",
      "timezone": "string",
      "lang": "string",
      "country": "string",
      "hasNft": boolean,
      "balances": [
        {
          "kind": "string",
          "amount": number
        }
      ]
    }
  }
}
```

#### Status Codes

| Status Code | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| 200         | Success - Restituisce il profilo dell'utente                 |
| 401         | Unauthorized - Token di autenticazione mancante o non valido |
| 500         | Internal Server Error - Errore del server                    |

### Update User Profile

Aggiorna i dati del profilo dell'utente autenticato.

#### Request

```http
PUT /api/v1/user
```

#### Request Body

```json
{
  "first_name": "string",
  "last_name": "string",
  "nickname": "string",
  "gender": "string",
  "birthdate": "string",
  "country": "string",
  "lang": "string",
  "timezone": "string",
  "profileImage": "string"
}
```

#### Response

```json
{
  "data": {
    "userId": "string",
    "type": "user",
    "attributes": {
      "first_name": "string",
      "last_name": "string",
      "nickname": "string",
      "updated_at": "string"
    }
  }
}
```

#### Status Codes

| Status Code | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| 200         | Success - Profilo utente aggiornato con successo             |
| 400         | Bad Request - Parametri mancanti o non validi                |
| 401         | Unauthorized - Token di autenticazione mancante o non valido |
| 500         | Internal Server Error - Errore del server                    |

### Get User Balances

Recupera i saldi dell'utente per le varie valute del sistema.

#### Request

```http
GET /api/v1/user/balances
```

#### Response

```json
{
  "data": {
    "items": [
      {
        "kind": "string",
        "amount": number,
        "nextRestoreAt": "string"
      }
    ]
  }
}
```

#### Status Codes

| Status Code | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| 200         | Success - Restituisce i saldi dell'utente                    |
| 401         | Unauthorized - Token di autenticazione mancante o non valido |
| 500         | Internal Server Error - Errore del server                    |

#### Note

- Il campo `kind` nei saldi può essere uno dei seguenti valori:
  - `exp`: Punti esperienza
  - `awc`: Valuta del gioco
  - `life`: Vite del gioco
- Il campo `nextRestoreAt` indica quando il saldo verrà ripristinato automaticamente (se applicabile)
