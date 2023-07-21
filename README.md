# Game Architecture

Below is a high-level overview of the game's architecture.

```plaintext
Client-side (Angular App)  <----> | .NET REST API on Azure PaaS App Service | <----> Azure SQL Database
                                  |     (Load Balanced and Traffic Managed)  | <----> Azure Storage <----|
                                  |                                        | <----> Azure CosmosDB    |
                                  |                                        |                          |
                                  |------------------> ChatGPT API          |   Azure Functions <------|
                                  |                                        |
                                  |------------------> Azure Event Hubs (Kafka Interface)
                                                        |
                                                        V
                                                  Azure DataBricks (Apache Spark)
## Components
Client-side (Angular App): The front-end of the game where users interact with the game UI.

.NET REST API on Azure PaaS App Service: The server-side of the application handles the game logic, and manages interactions with the Azure SQL database and Azure Storage.

Azure SQL Database: A fully managed relational database that is used for storing game-related data, including player information, in-game assets, game states, etc.

Azure Storage: The battles in the game are recorded in JSON format and stored in Azure Storage. The creation of new blob triggers Azure Functions.

Azure CosmosDB: A NoSQL database for storing unstructured data or data that doesn't fit well into a relational model.

ChatGPT API: Integrated to enhance the game experience by generating interactive dialogues with NPCs, or providing a help center for users within the game.

Azure Functions: Detects the creation of new blobs in Azure Storage, parse these files, and emit events into Azure Event Hubs.

Azure Event Hubs (with Kafka interface): A real-time data ingestion service that takes in events from Azure Functions and makes them available for consumption.

Azure Databricks (Apache Spark): Provides a fast, easy, and collaborative Apache Spark-based analytics platform for real-time analytics on the events consumed from Azure Event Hubs.
