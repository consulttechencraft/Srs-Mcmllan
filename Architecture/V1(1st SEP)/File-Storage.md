```mermaid
flowchart TD
    User[User Uploads PDF] --> App[Backend App]
    App -->|Upload File| S3[(S3 Bucket)]
    App -->|INSERT INTO documents (s3_key)| Postgres[(PostgreSQL DB)]
    
    User2[User Downloads PDF] --> App
    App -->|Fetch s3_key FROM DB| Postgres
    App -->|Get File via s3_key| S3
    App -->|Return PDF| User2
