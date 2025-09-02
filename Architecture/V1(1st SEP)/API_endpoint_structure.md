```mermaid
graph TD
    %% Main API Gateway
    API[McMillan Enterprise API v1]
    
    %% Authentication & Authorization Module
    subgraph AUTH["🔐 Authentication & Authorization"]
        AUTH_USER[User Authentication<br/>Login, Register, Logout<br/>Password Reset, Email Verify]
        AUTH_2FA[Two-Factor Authentication<br/>Enable, Disable, Verify 2FA]
        AUTH_SSO[Single Sign-On Enterprise<br/>SSO Providers & Callbacks]
    end
    
    %% User & Organization Management
    subgraph USER["👥 User & Organization Management"]
        USER_PROFILE[User Profile<br/>Profile & Settings Management<br/>Activity Logging]
        USER_TEAM[Team Management<br/>Member Operations<br/>Invitations & Roles]
        USER_RBAC[Role-Based Access Control<br/>Roles & Permissions<br/>Custom Role Creation]
    end
    
    %% Invoice Management
    subgraph INVOICE["📄 Invoice Management"]
        INVOICE_OPS[Invoice Operations<br/>Upload, CRUD Operations<br/>AI Processing Trigger]
        INVOICE_BULK[Bulk Operations<br/>Multi-Invoice Processing<br/>Batch Updates & Deletes]
        INVOICE_DATA[Data Extraction<br/>AI-Extracted Data<br/>Validation & Confidence]
    end
    
    %% Data Processing & Validation
    subgraph PROCESS["⚙️ Data Processing & Validation"]
        PROCESS_VALIDATION[Data Validation<br/>Approval & Rejection<br/>Manual Corrections]
        PROCESS_QUEUE[Processing Queue<br/>Queue Management<br/>Priority Processing]
    end
    
    %% Bank Reconciliation
    subgraph BANK["🏦 Bank Reconciliation"]
        BANK_RECON[Reconciliation Operations<br/>Report Creation<br/>Export Capabilities]
        BANK_INTEGRATION[Bank Data Integration<br/>Account Connection<br/>Transaction Sync]
    end
    
    %% Analytics & Reporting
    subgraph ANALYTICS["📊 Analytics & Reporting"]
        ANALYTICS_DASH[Dashboard Data<br/>Overview & Metrics<br/>Team Workload]
        ANALYTICS_DATA[Analytics Engine<br/>Trends & Analysis<br/>Accuracy Metrics]
        ANALYTICS_REPORTS[Custom Reports<br/>Report Creation<br/>Scheduled Delivery]
    end
    
    %% Integrations
    subgraph INTEGRATIONS["🔗 Integrations"]
        INTEGRATIONS_ACCOUNTING[Accounting Software<br/>QuickBooks, Xero<br/>NetSuite, SAP]
        INTEGRATIONS_CUSTOM[Custom API Enterprise<br/>Webhooks Management<br/>Custom Endpoints]
        INTEGRATIONS_SYNC[Data Synchronization<br/>Sync Operations<br/>Status & History]
    end
    
    %% Subscription & Billing
    subgraph BILLING["💳 Subscription & Billing"]
        BILLING_SUB[Subscription Management<br/>Plan Upgrades<br/>Billing Cycle Changes]
        BILLING_USAGE[Usage Tracking<br/>Monthly Usage<br/>Limits & Alerts]
        BILLING_PAY[Payment Management<br/>Payment Methods<br/>Billing History]
    end
    
    %% Notifications
    subgraph NOTIFICATIONS["🔔 Notifications & Communication"]
        NOTIF_MANAGE[Notification Management<br/>Read Status<br/>User Preferences]
        NOTIF_ALERTS[Custom Alerts<br/>Alert Configuration<br/>Email Notifications]
    end
    
    %% Support
    subgraph SUPPORT["🎧 Support & Help"]
        SUPPORT_TICKETS[Support System<br/>Ticket Management<br/>Message Threading]
        SUPPORT_KB[Knowledge Base<br/>Help Articles<br/>Feedback System]
    end
    
    %% Security & Compliance
    subgraph SECURITY["🛡️ Security & Compliance"]
        SECURITY_SETTINGS[Security Management<br/>Session Control<br/>API Key Management]
        SECURITY_AUDIT[Audit & Compliance<br/>Audit Logs Enterprise<br/>Data Export GDPR]
    end
    
    %% File Management
    subgraph FILES["📁 File Management"]
        FILES_OPS[File Operations<br/>Upload & Download<br/>Metadata Management]
        FILES_DOC[Document Processing<br/>OCR Processing<br/>Data Extraction]
    end
    
    %% External Services
    OPENAI[OpenAI API<br/>AI Processing]
    ACCOUNTING_SYS[Accounting Systems<br/>QuickBooks, Xero<br/>NetSuite, SAP]
    BANKING_API[Banking APIs<br/>Transaction Data]
    
    %% Main API connections
    API --> AUTH
    API --> USER
    API --> INVOICE
    API --> PROCESS
    API --> BANK
    API --> ANALYTICS
    API --> INTEGRATIONS
    API --> BILLING
    API --> NOTIFICATIONS
    API --> SUPPORT
    API --> SECURITY
    API --> FILES
    
    %% Internal module connections
    AUTH --> USER_PROFILE
    AUTH --> USER_TEAM
    AUTH --> USER_RBAC
    
    USER --> INVOICE_OPS
    INVOICE_OPS --> INVOICE_BULK
    INVOICE_OPS --> INVOICE_DATA
    
    INVOICE_DATA --> PROCESS_VALIDATION
    INVOICE_DATA --> PROCESS_QUEUE
    
    PROCESS_VALIDATION --> ANALYTICS_DATA
    BANK_RECON --> ANALYTICS_DATA
    
    %% External service connections
    INTEGRATIONS_ACCOUNTING --> ACCOUNTING_SYS
    BANK_INTEGRATION --> BANKING_API
    PROCESS_QUEUE --> OPENAI
    FILES_DOC --> OPENAI
    
    %% Cross-functional relationships
    SECURITY_SETTINGS --> AUTH_USER
    NOTIF_MANAGE --> PROCESS_VALIDATION
    ANALYTICS_REPORTS --> BILLING_USAGE
    
    %% API Design Principles Box
    subgraph PRINCIPLES["⚙️ API Design Principles"]
        REST[RESTful Design<br/>Standard HTTP Methods<br/>JSON Format]
        PAGINATION[Pagination & Filtering<br/>Standard Parameters<br/>Sorting Support]
        VERSIONING[API Versioning<br/>Backward Compatibility<br/>Deprecation Management]
        SECURITY_PRIN[Security Standards<br/>JWT Authentication<br/>Rate Limiting]
    end
    
    API --> PRINCIPLES
    
    %% Styling
    classDef authModule fill:#FF6B6B,stroke:#fff,stroke-width:2px,color:#fff
    classDef userModule fill:#4ECDC4,stroke:#fff,stroke-width:2px,color:#fff
    classDef invoiceModule fill:#45B7D1,stroke:#fff,stroke-width:2px,color:#fff
    classDef processModule fill:#FFA07A,stroke:#fff,stroke-width:2px,color:#fff
    classDef bankModule fill:#98D8C8,stroke:#fff,stroke-width:2px,color:#fff
    classDef analyticsModule fill:#F7DC6F,stroke:#333,stroke-width:2px,color:#333
    classDef integrationModule fill:#BB8FCE,stroke:#fff,stroke-width:2px,color:#fff
    classDef billingModule fill:#85C1E9,stroke:#fff,stroke-width:2px,color:#fff
    classDef notificationModule fill:#F8C471,stroke:#333,stroke-width:2px,color:#333
    classDef supportModule fill:#82E0AA,stroke:#fff,stroke-width:2px,color:#fff
    classDef securityModule fill:#EC7063,stroke:#fff,stroke-width:2px,color:#fff
    classDef fileModule fill:#D7BDE2,stroke:#fff,stroke-width:2px,color:#fff
    classDef external fill:#AED6F1,stroke:#333,stroke-width:2px,color:#333
    classDef main fill:#2C3E50,stroke:#fff,stroke-width:3px,color:#fff
    classDef principles fill:#E8F8F5,stroke:#27AE60,stroke-width:2px,color:#27AE60
    
    class AUTH authModule
    class USER userModule
    class INVOICE invoiceModule
    class PROCESS processModule
    class BANK bankModule
    class ANALYTICS analyticsModule
    class INTEGRATIONS integrationModule
    class BILLING billingModule
    class NOTIFICATIONS notificationModule
    class SUPPORT supportModule
    class SECURITY securityModule
    class FILES fileModule
    class OPENAI,ACCOUNTING_SYS,BANKING_API external
    class API main
    class PRINCIPLES principles
