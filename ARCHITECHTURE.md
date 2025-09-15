```mermaid
graph TD
    subgraph "Client Tier"
        A["Mobile App \n(React Native)"]
    end

    subgraph "API & Gateway Tier"
        B["API Gateway \n(Handles Auth & Routing)"]
    end

    subgraph "Core Microservices"
        C["User Service \n(Node.js)"]
        D["Location Service \n(Go)"]
        E["Matching Service \n(Go)"]
        F["Trip Service \n(Node.js)"]
        G["Chat Service \n(Node.js)"]
        H["Notification Service \n(Node.js)"]
    end

    subgraph "Asynchronous Backbone"
        I["Message Broker \n(RabbitMQ)"]
    end

    subgraph "Data Tier"
        J["PostgreSQL + PostGIS \n(Primary DB)"]
        K["Redis Cache \n(Real-time Locations)"]
    end

    %% --- Connections ---
    A --> B

    B --> C
    B --> D
    B --> E
    B --> F
    B --> G

    E --> I
    F --> I
    I --> H

    H --> A

    C --> J
    D --> K
    E --> K
    E --> J
    F --> J
    G --> J
