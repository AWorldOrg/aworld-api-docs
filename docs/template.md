## [Nome Entità] API

Questa sezione descrive gli endpoint REST API per la gestione di [descrizione entità].

### [Nome Operazione]

[Breve descrizione dell'operazione]

#### Request

```http
[METODO HTTP] /v1/[path]
```

#### Query Parameters

| Parameter | Type   | Required | Description               |
| --------- | ------ | -------- | ------------------------- |
| param1    | string | Yes/No   | Descrizione del parametro |
| param2    | number | Yes/No   | Descrizione del parametro |

#### Response

```json
{
  "data": {
    // Struttura della risposta
    "field1": "tipo_e_descrizione",
    "field2": 0,
    "arrayField": [
      {
        "subField1": "tipo_e_descrizione",
        "subField2": "tipo_e_descrizione"
      }
    ]
  }
}
```

#### Status Codes

| Status Code | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| 200         | Success - [Descrizione del successo]                         |
| 400         | Bad Request - Parametri mancanti o non validi                |
| 401         | Unauthorized - Token di autenticazione mancante o non valido |
| 403         | Forbidden - L'utente non ha i permessi necessari             |
| 500         | Internal Server Error - Errore del server                    |

#### Note

- [Nota importante 1]
- [Nota importante 2]
- [Eventuali limitazioni o comportamenti specifici]
