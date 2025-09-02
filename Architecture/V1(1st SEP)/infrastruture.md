```mermaid
graph TB
    %% External Services
    OpenAI[OpenAI API]
    Users[Users/Clients]
    
    %% AWS Cloud
    subgraph AWS["AWS Cloud"]
        %% S3 Buckets
        subgraph S3["Amazon S3"]
            S3Frontend1[Frontend App 1<br/>Static Website]
            S3Frontend2[Frontend App 2<br/>Static Website]
            S3Data[Document Storage<br/>10 GiB]
        end
        
        %% EC2 Instance
        subgraph EC2["EC2 t3.medium<br/>2 vCPUs, 4 GiB RAM"]
            %% Docker Network
            subgraph Docker["Docker Network (mcmillan-net)"]
                Nginx[Nginx<br/>Port 80/443<br/>Reverse Proxy & Load Balancer]
                FastAPI[FastAPI Backend<br/>Port 8000<br/>REST API & Auth]
                InvoiceAI[InvoiceAI Service<br/>Port 8001<br/>OCR & AI Processing]
                Postgres[PostgreSQL 15<br/>Port 5432<br/>Database]
                pgAdmin[pgAdmin<br/>Port 5050<br/>DB Management]
            end
        end
        
        %% EBS Volume
        EBS[EBS Volume<br/>20 GiB gp3<br/>Persistent Storage]
        
        %% CloudWatch
        CloudWatch[CloudWatch<br/>Monitoring & Logging]
    end
    
    %% External connections
    Users --> S3Frontend1
    Users --> S3Frontend2
    Users --> Nginx
    
    %% S3 connections
    S3Frontend1 --> Nginx
    S3Frontend2 --> Nginx
    
    %% Nginx routing
    Nginx --> FastAPI
    Nginx --> InvoiceAI
    Nginx --> pgAdmin
    
    %% Docker container connections
    FastAPI --> Postgres
    InvoiceAI --> Postgres
    InvoiceAI --> OpenAI
    FastAPI --> S3Data
    
    %% Storage connections
    EC2 --> EBS
    Postgres -.-> EBS
    FastAPI -.-> EBS
    
    %% Monitoring
    EC2 --> CloudWatch
    
    %% Styling
    classDef awsService fill:#FF9900,stroke:#232F3E,stroke-width:2px,color:#fff
    classDef dockerContainer fill:#2496ED,stroke:#fff,stroke-width:2px,color:#fff
    classDef storage fill:#3F48CC,stroke:#fff,stroke-width:2px,color:#fff
    classDef external fill:#28A745,stroke:#fff,stroke-width:2px,color:#fff
    
    class AWS,EC2,S3,EBS,CloudWatch awsService
    class FastAPI,InvoiceAI,Postgres,pgAdmin,Nginx dockerContainer
    class S3Frontend1,S3Frontend2,S3Data storage
    class OpenAI,Users external 
