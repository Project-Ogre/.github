# Game Architecture

High-level overview of how District Ogre is hosted and how data moves through the system.

```plaintext
Player (Angular App)
        |
        v
Azure Static Web Apps (UI)
        |
        v
Azure App Service (ASP.NET Core API)
   |         |            |
   v         v            v
Azure SQL   Azure Storage   Azure SignalR
            (blobs/queues)
```

## Components

### UI (Angular App)
Players manage characters, parties, inventory, shops, districts, and skirmishes (PvE/PvP).  
Live UI: [District Ogre](https://zealous-mud-0ef58d91e.5.azurestaticapps.net/)

### API (Azure App Service)
A modular ASP.NET Core API handles game logic and persistence for players, characters, parties, inventory, districts, and skirmishes. In-process workers process district turns and related background work.  
Live API: [District Ogre API](https://project-ogre-api.azurewebsites.net/)

### Azure SQL Database
Primary store for game state: players, characters, parties, inventory, districts, ladders, and related progress.

### Azure Storage
Blob storage holds skirmish battle payloads used for replay. Storage queues can carry district turn messages when not processed in-process by the API.

### Azure SignalR
Pushes live district updates to connected clients (e.g. map / turn state).
