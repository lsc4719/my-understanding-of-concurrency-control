## Optimistic Lock

```mermaid
sequenceDiagram
    participant Alice
    participant Bob
    participant Resource

    Note over Alice,Bob: Optimism: There will be no conflict

    Alice->>Resource: read version
    Resource-->>Alice: v1

    Note over Alice: uncommitted changes

    Bob->>Resource: read version v1
    Resource-->>Bob: v1

    Note over Bob: uncommitted changes

    Alice->>Resource: CAS: if version==v1 then set version=v2 and commit
    Resource-->>Alice: commit success
    Note right of Resource: version = v2

    Bob->>Resource: CAS: if version==v1 then set version=v2 and commit
    Resource-->>Bob: commit failed (Optimistic Lock Conflict)

    Note over Bob: transaction rolled back and retry...

```

## Pessimistic Lock

exclusive access
