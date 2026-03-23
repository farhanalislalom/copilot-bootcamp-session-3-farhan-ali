# Cloud Architecture Overview

This monorepo runs as a simple single-environment system with:
- A React frontend for task management UI
- An Express API for task CRUD operations
- An in-memory SQLite store for runtime task persistence

## System Context Diagram

```mermaid
flowchart LR
    U[User]
    FE[React Frontend]
    API[Express API]
    DB[(In-Memory Store)]

    U -->|Browser UI| FE
    FE -->|HTTP JSON /api/tasks| API
    API -->|Read/Write Tasks| DB
    DB -->|Task Rows| API
    API -->|JSON Responses| FE
```

### Text Diagram (Fallback)

```text
+--------+        Browser UI        +----------------+      /api/tasks      +--------------+
|  User  | -----------------------> | React Frontend | -------------------> | Express API  |
+--------+                          +----------------+                      +------+-------+
                                                                               | Read/Write |
                                                                               v            |
                                                                         +------------------+
                                                                         | In-Memory Store  |
                                                                         |  SQLite (:memory:)|
                                                                         +------------------+
```

## Create TODO Flow Diagram

```mermaid
flowchart LR
        U[User]

        subgraph FE[React Frontend]
            FE1[Fill form and click Add Task]
            FE2{Title valid?}
            FE3[Show validation error]
            FE4[Send POST /api/tasks]
            FE5[Fetch refreshed task list]
            FE6[Render updated TODO list]
        end

        subgraph API[Express API]
            AP1[Validate request]
            AP2[Insert task row]
            AP3[Read created task]
            AP4[Return 201 Created]
            AP5[Handle GET /api/tasks]
            AP6[Return 200 OK with tasks]
        end

        subgraph DB[In-Memory SQLite]
            DB1[(tasks table)]
        end

        U --> FE1 --> FE2
        FE2 -- No --> FE3
        FE2 -- Yes --> FE4 --> AP1 --> AP2 --> DB1 --> AP3 --> DB1 --> AP4 --> FE5
        FE5 --> AP5 --> DB1 --> AP6 --> FE6 --> U
```

## Notes

- The frontend and backend are developed in the same monorepo.
- The backend uses in-memory storage, so data resets when the process restarts.
- No external cloud database or third-party storage service is part of this architecture.
