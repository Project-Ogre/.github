# Game Architecture

Below is a high-level overview of the game's architecture.

```plaintext
Client-side (Angular App)  <----> | .NET REST API on Azure PaaS App Service | <----> Azure SQL Database
                                  |     (Load Balanced and Traffic Managed)  | <----> Azure Storage
                                  |                                        | <----> Azure CosmosDB (Optional)
                                  |
                                  |------------------> ChatGPT API
