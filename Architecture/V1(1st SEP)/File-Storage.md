```mermaid
flowchart TD
    User[User Uploads PDF] --> App[Backend App]
    App -->|Upload File| S3[S3 Bucket]
    App -->|Insert metadata + S3 key| Postgres[PostgreSQL DB]

    User2[User Downloads PDF] --> App
    App -->|Fetch S3 key from DB| Postgres
    App -->|Get File via S3 key| S3
    App -->|Return PDF| User2
