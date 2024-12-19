## AWorld REST API Documentation

### Introduzione

**AWorld** è una piattaforma digitale pensata per promuovere la **sostenibilità** e il **coinvolgimento degli utenti** attraverso strumenti innovativi e contenuti personalizzati. Selezionata dalle **Nazioni Unite** per la campagna **ActNow**, AWorld supporta organizzazioni e individui nell'adozione di comportamenti sostenibili e nella riduzione della propria impronta ambientale.

Il cuore della piattaforma è l'**applicazione mobile AWorld**, disponibile negli store iOS e Android, che offre un'esperienza completa di engagement e monitoraggio della sostenibilità. Parallelamente, AWorld mette a disposizione il proprio **ecosistema di misurazione, engagement e contenuti** attraverso API che permettono a terze parti di integrare le meccaniche e le funzionalità della piattaforma nei propri sistemi.

La piattaforma si presenta come una **soluzione flessibile e integrabile**, capace di adattarsi alle esigenze di aziende, istituzioni e partner tecnologici.

La presente documentazione descrive le **API REST di consumo** della piattaforma AWorld, fornendo gli strumenti necessari per l'integrazione delle funzionalità core nei sistemi client. Si noti che queste API sono specificamente progettate per le **operazioni di utilizzo della piattaforma**; le funzionalità di amministrazione e gestione del tenant sono oggetto di una documentazione separata.

Il sistema fornisce un'API REST completa che permette agli utenti di partecipare a varie attività, completare missioni, interagire con contenuti educativi e far parte di comunità attive.

#### Caratteristiche Principali

- **Autenticazione Multi-tenant**: Supporto per diversi metodi di autenticazione e gestione utenti
- **Gestione Contenuti**: Stories e quiz interattivi per l'apprendimento
- **Sistema di Progressione**: Tracciamento delle attività e sistema di ricompense
- **Funzionalità Social**: Comunità e missioni collaborative
- **Calendario Attività**: Monitoraggio giornaliero delle attività e streak

#### Architettura API

L'API è organizzata in modo modulare, con endpoint specifici per ogni dominio funzionale:

1. **Core Services**: Autenticazione e gestione utenti
2. **Activity Tracking**: Calendario e monitoraggio progressi
3. **Content Services**: Stories e quiz
4. **Engagement Services**: Azioni e missioni
5. **Social Services**: Comunità e missioni comunitarie

### Documentazione API

| Sezione                | File                                                     | Endpoints                                                            |
| ---------------------- | -------------------------------------------------------- | -------------------------------------------------------------------- |
| **Authentication**     | [authentication.md](./docs/01-authentication.md)         | Headers richiesti, formati risposta, codici stato, rate limiting     |
| **Users**              | [users.md](./docs/02-users.md)                           | Get/Update Profile, Get Level, Get Balances, Delete Account          |
| **Calendar**           | [calendar.md](./docs/03-calendar.md)                     | Get Daily Calendar, Get Calendar Preview, Get Monthly Streak         |
| **Stories**            | [stories.md](./docs/04-stories.md)                       | Get/List Stories, Submit Progress, Stories Feedback, Popular Stories |
| **Quiz**               | [quiz.md](./docs/05-quiz.md)                             | Get Quiz, Get Random Quiz, Submit Quiz Answer                        |
| **Actions**            | [actions.md](./docs/06-actions.md)                       | Get/List Actions, Submit Action, Search Actions                      |
| **Missions**           | [missions.md](./docs/07-missions.md)                     | Get/List Missions, Submit Mission Progress                           |
| **Communities**        | [communities.md](./docs/08-communities.md)               | Get/List Communities, Join Community, Community Members              |
| **Community Missions** | [community-missions.md](./docs/09-community-missions.md) | Get/List CommunityMissions, Join CommunityMission, Leaderboard       |

### Specifiche Tecniche

#### Autenticazione
Tutte le richieste richiedono i seguenti headers:
- `x-aw-tenant`: Identificatore dell'istanza Client
- `x-aw-uid`: Identificatore valido dell'utente nella piattaforma Client

#### Formato Dati
| Tipo         | Formato                               |
| ------------ | ------------------------------------- |
| Content-Type | application/json                      |
| Accept       | application/json                      |
| Date         | ISO 8601 (es. "2024-01-01T12:00:00Z") |
| ID           | String                                |
| Numbers      | Integer o Float                       |
| Boolean      | true/false                            |
| Arrays       | JSON arrays                           |
| Objects      | JSON objects                          |

#### URL Base
Tutti gli endpoint iniziano con:
```
https://api.example.com/v1
```

#### Paginazione
La paginazione è supportata negli endpoint di lista con i seguenti parametri:

| Parametro | Descrizione                    |
| --------- | ------------------------------ |
| limit     | Numero di elementi per pagina  |
| nextToken | Token per la pagina successiva |

#### Rate Limiting
- Headers di rate limit inclusi in tutte le risposte
- Limiti applicati per utente
- Vedere la documentazione di autenticazione per i dettagli

#### Best Practices
- Utilizzare HTTPS per tutte le richieste
- Implementare gestione degli errori robusta
- Rispettare i limiti di rate
- Utilizzare la paginazione per liste lunghe
- Mantenere le sessioni utente sicure
- Validare tutti i dati di input
- Gestire correttamente i timeout

#### Note
- Le risposte sono sempre in formato JSON
- Gli errori seguono un formato standard
- La paginazione è consistente in tutti gli endpoint di lista
- I timestamp seguono sempre il formato ISO 8601
- Le richieste non valide ricevono risposte di errore dettagliate
