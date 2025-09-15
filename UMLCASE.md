```mermaid
graph TD
    subgraph Varcity System
        uc1(Register & Verify)
        uc2(Manage Profile)
        uc3(Request Ride)
        uc4(Offer Ride)
        uc5(Chat with Match)
        uc6(Track Trip in Real-time)
        uc7(Rate Peer)
    end

    Rider["Student (Rider)"]
    Driver["Student (Driver)"]

    Rider --> uc1
    Rider --> uc2
    Rider --> uc3
    Rider --> uc5
    Rider --> uc6
    Rider --> uc7

    Driver --> uc1
    Driver --> uc2
    Driver --> uc4
    Driver --> uc5
    Driver --> uc6
    Driver --> uc7
