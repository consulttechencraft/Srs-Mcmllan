```mermaid
graph TD
    %% Main API Gateway
    API[McMillan Enterprise API<br/>v1]
    
    %% Authentication & Authorization Module
    subgraph AUTH["🔐 Authentication & Authorization"]
        AUTH_USER[User Authentication<br/>POST /auth/register<br/>POST /auth/login<br/>POST /auth/logout<br/>POST /auth/refresh<br/>POST /auth/forgot-password<br/>POST /auth/reset-password<br/>POST /auth/verify-email]
        
        AUTH_2FA[Two-Factor Authentication<br/>POST /auth/2fa/enable<br/>POST /auth/2fa/disable<br/>POST /auth/2fa/verify]
        
        AUTH_SSO[Single Sign-On Enterprise<br/>GET /auth/sso/providers<br/>POST /auth/sso/initiate<br/>POST /auth/sso/callback]
    end
    
    %% User & Organization Management
    subgraph USER["👥 User & Organization Management"]
        USER_PROFILE[User Profile<br/>GET /users/profile<br/>PUT /users/profile<br/>GET /users/settings<br/>PUT /users/settings<br/>GET /users/activity-log]
        
        USER_TEAM[Team Management<br/>GET /organizations/{org_id}/members<br/>POST /organizations/{org_id}/members<br/>PUT /organizations/{org_id}/members/{user_id}<br/>DELETE /organizations/{org_id}/members/{user_id}]
        
        USER_RBAC[Role-Based Access Control<br/>GET /roles<br/>GET /permissions<br/>POST /organizations/{org_id}/roles<br/>PUT /organizations/{org_id}/roles/{role_id}]
    end
    
    %% Invoice Management
    subgraph INVOICE["📄 Invoice Management"]
        INVOICE_OPS[Invoice Operations<br/>POST /invoices/upload<br/>GET /invoices<br/>GET /invoices/{invoice_id}<br/>PUT /invoices/{invoice_id}<br/>DELETE /invoices/{invoice_id}<br/>POST /invoices/{invoice_id}/process]
        
        INVOICE_BULK[Bulk Operations<br/>POST /invoices/bulk-upload<br/>POST /invoices/bulk-process<br/>PUT /invoices/bulk-update<br/>DELETE /invoices/bulk-delete]
        
        INVOICE_DATA[Data Extraction<br/>GET /invoices/{invoice_id}/extracted-data<br/>PUT /invoices/{invoice_id}/extracted-data<br/>POST /invoices/{invoice_id}/validate<br/>GET /invoices/{invoice_id}/confidence-score]
    end
    
    %% Data Processing & Validation
    subgraph PROCESS["⚙️ Data Processing & Validation"]
        PROCESS_VALIDATION[Data Validation<br/>GET /data-validation/pending<br/>POST /data-validation/{item_id}/approve<br/>POST /data-validation/{item_id}/reject<br/>PUT /data-validation/{item_id}/correct]
        
        PROCESS_QUEUE[Processing Queue<br/>GET /processing/queue<br/>POST /processing/priority/{invoice_id}<br/>GET /processing/history]
    end
    
    %% Bank Reconciliation
    subgraph BANK["🏦 Bank Reconciliation"]
        BANK_RECON[Reconciliation Operations<br/>POST /reconciliation/create<br/>GET /reconciliation/reports<br/>GET /reconciliation/reports/{report_id}<br/>PUT /reconciliation/reports/{report_id}]
        
        BANK_INTEGRATION[Bank Data Integration<br/>GET /bank-accounts<br/>POST /bank-accounts/connect<br/>DELETE /bank-accounts/{account_id}<br/>POST /bank-accounts/{account_id}/sync]
    end
    
    %% Analytics & Reporting
    subgraph ANALYTICS["📊 Analytics & Reporting"]
        ANALYTICS_DASH[Dashboard Data<br/>GET /dashboard/overview<br/>GET /dashboard/recent-activity<br/>GET /dashboard/processing-metrics<br/>GET /dashboard/team-workload]
        
        ANALYTICS_DATA[Analytics<br/>GET /analytics/invoice-trends<br/>GET /analytics/vendor-analysis<br/>GET /analytics/processing-time<br/>GET /analytics/accuracy-metrics]
        
        ANALYTICS_REPORTS[Custom Reports<br/>POST /reports/create<br/>GET /reports<br/>GET /reports/{report_id}<br/>PUT /reports/{report_id}<br/>POST /reports/{report_id}/schedule]
    end
    
    %% Integrations
    subgraph INTEGRATIONS["🔗 Integrations"]
        INTEGRATIONS_ACCOUNTING[Accounting Software<br/>GET /integrations/available<br/>POST /integrations/quickbooks/connect<br/>POST /integrations/xero/connect<br/>POST /integrations/netsuite/connect<br/>POST /integrations/sap/connect]
        
        INTEGRATIONS_CUSTOM[Custom API Enterprise<br/>POST /integrations/custom/webhook<br/>GET /integrations/custom/webhooks<br/>PUT /integrations/custom/webhooks/{webhook_id}]
        
        INTEGRATIONS_SYNC[Data Sync<br/>POST /integrations/{integration_id}/sync<br/>GET /integrations/{integration_id}/sync-status<br/>GET /integrations/{integration_id}/sync-history]
    end
    
    %% Subscription & Billing
    subgraph BILLING["💳 Subscription & Billing"]
        BILLING_SUB[Subscription Management<br/>GET /subscription/current<br/>POST /subscription/upgrade<br/>POST /subscription/downgrade<br/>PUT /subscription/billing-cycle]
        
        BILLING_USAGE[Usage Tracking<br/>GET /usage/current-month<br/>GET /usage/history<br/>GET /usage/limits<br/>POST /usage/alerts]
        
        BILLING_PAY[Billing<br/>GET /billing/invoices<br/>GET /billing/payment-methods<br/>POST /billing/payment-methods<br/>PUT /billing/payment-methods/{method_id}]
    end
    
    %% Notifications
    subgraph NOTIFICATIONS["🔔 Notifications & Communication"]
        NOTIF_MANAGE[Notifications<br/>GET /notifications<br/>PUT /notifications/{notification_id}/read<br/>POST /notifications/mark-all-read<br/>PUT /notifications/settings]
        
        NOTIF_ALERTS[Email & Alerts<br/>POST /alerts/create<br/>GET /alerts<br/>PUT /alerts/{alert_id}<br/>DELETE /alerts/{alert_id}]
    end
    
    %% Support
    subgraph SUPPORT["🎧 Support & Help"]
        SUPPORT_TICKETS[Support Tickets<br/>POST /support/tickets<br/>GET /support/tickets<br/>GET /support/tickets/{ticket_id}<br/>PUT /support/tickets/{ticket_id}]
        
        SUPPORT_KB[Knowledge Base<br/>GET /help/articles<br/>GET /help/articles/{article_id}<br/>GET /help/categories<br/>POST /help/feedback]
    end
    
    %% Security & Compliance
    subgraph SECURITY["🛡️ Security & Compliance"]
        SECURITY_SETTINGS[Security Settings<br/>GET /security/sessions<br/>DELETE /security/sessions/{session_id}<br/>GET /security/login-history<br/>POST /security/api-keys]
        
        SECURITY_AUDIT[Audit & Compliance<br/>GET /audit/logs<br/>POST /compliance/export-data<br/>POST /compliance/delete-data<br/>GET /compliance/certifications]
    end
    
    %% File Management
    subgraph FILES["📁 File Management"]
        FILES_OPS[File Operations<br/>POST /files/upload<br/>GET /files/{file_id}<br/>DELETE /files/{file_id}<br/>GET /files/{file_id}/metadata]
        
        FILES_DOC[Document Processing<br/>POST /documents/ocr<br/>GET /documents/{doc_id}/preview<br/>POST /documents/{doc_id}/extract]
    end
    
    %% External Services
    OPENAI[OpenAI API<br/>AI Processing]
    ACCOUNTING[Accounting Systems<br/>QuickBooks, Xero, NetSuite, SAP]
    BANKS[Banking APIs<br/>Transaction Data]
    
    %% Main connections
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
    
    %% Cross-module relationships
    AUTH --> USER
    USER --> INVOICE
    INVOICE --> PROCESS
    INVOICE --> FILES_DOC
    PROCESS --> ANALYTICS
    BANK --> ANALYTICS
    INTEGRATIONS --> ACCOUNTING
    BANK --> BANKS
    PROCESS --> OPENAI
    INVOICE --> OPENAI
    
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
    class OPENAI,ACCOUNTING,BANKS external
    class API main
