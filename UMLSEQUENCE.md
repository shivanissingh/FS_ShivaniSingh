```mermaid
sequenceDiagram
    participant Client as Mobile App
    participant API Gateway
    participant MatchingService as Matching Service (Go)
    participant Redis as Redis Cache
    participant PostgresDB as PostgreSQL DB
    participant NotificationService as Notification Service

    Client->>API Gateway: POST /findMatch (auth_token, start, end)
    activate API Gateway
    API Gateway->>MatchingService: findMatches(user_id, start, end)
    deactivate API Gateway
    activate MatchingService

    MatchingService->>Redis: getDriversInGeohashes(geohashes)
    activate Redis
    Redis-->>MatchingService: [nearby_driver_ids]
    deactivate Redis

    MatchingService->>PostgresDB: getFullRoutesForDrivers(ids)
    activate PostgresDB
    PostgresDB-->>MatchingService: [driver_routes]
    deactivate PostgresDB

    MatchingService->>MatchingService: Run filtering & ranking logic
    
    MatchingService->>NotificationService: notifyUserOfMatch(user_id, match)
    activate NotificationService
    NotificationService-->>Client: <<Push Notification>> Match Found!
    deactivate NotificationService
    
    MatchingService-->>Client: 200 OK {matches: [...]}
    deactivate MatchingService
