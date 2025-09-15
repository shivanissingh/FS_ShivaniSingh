# Data Flow — Sahyatri

## Overview
This document explains how a user's commute request flows through Sahyatri, the interactions between services, and the key synchronous and asynchronous paths. It contains both a visual diagram and a textual step-by-step walkthrough so reviewers can quickly understand system behavior.

---

## 1) High-level Dataflow (Mermaid)
```mermaid
graph TD
    %% Define Entities & Data Stores
    A[Student]
    DS1[(PostgreSQL DB)]
    DS2[(Redis Cache)]

    %% Define Processes
    P1{{1. Submit Ride Details}}
    P2{{2. Authenticate & Route Request}}
    P3{{3. Find Candidate Drivers}}
    P4{{4. Filter & Match Routes}}
    P5{{5. Notify Student}}

    %% Define Flows
    A -- "Pickup & Destination" --> P1;
    P1 -- "Request with User Token" --> P2;
    P2 -- "Validated Request" --> P3;
    P3 -- "Query by Geohash" --> DS2;
    DS2 -- "List of Nearby Driver IDs" --> P3;
    P3 -- "Candidate Driver IDs" --> P4;
    P4 -- "Fetch Driver Routes" --> DS1;
    DS1 -- "Full Route Data" --> P4;
    P4 -- "Confirmed Match Details" --> P5;
    P5 -- "Push Notification" --> A;
