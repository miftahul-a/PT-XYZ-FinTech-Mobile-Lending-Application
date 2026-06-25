# PT XYZ FinTech - Mobile Lending Application

## Solution Analyst Assessment

> \*\*Tech Stack\*\*: Enterprise Microservices, Cloud Native, Event-Driven
> (Kafka), PostgreSQL, Kubernetes.

\---
Author

**Miftahul Arifin**  
Business Analyst | System Analyst | Solution Analyst  
miftahularifin.id@gmail.com

\---

# ✅ Mapping Terhadap Soal Technical Test

\---

Soal Technical Test     Visual Assets            Alternatif Kode Mermaid

\---

**1. High Level Design  `01\_High\_Level\_Design\_Architecture.png`   Lihat Bagian 1
Architecture**

**2. Screen Flow \&      `03\_Screen\_Flow.png`, `04\_ERD.png`        Lihat Bagian 3 \& 4
ERD**

**3. Detail Design      `05\_API\_Design.png`,                      Lihat Bagian 5 \& 6
API**                   `06\_Sequence\_Diagram.png`

**4. Detail Screen      `07\_State\_Machine.png`,                   Lihat Bagian 7 \& 8
Behavior**              `08\_Wireframe\_Design.png`

**Tambahan**            `09\_Traceability\_Matrix.png`,             Lihat Bagian 9-11
`10\_Assumptions.png`, `11\_NFR.png`
---

\---

# 1\. HIGH LEVEL DESIGN ARCHITECTURE

!\[High Level](02\_Architecture\_Design/assets/01\_High\_Level\_Design\_Architecture.png)

``` mermaid
graph TD
Mobile\["Mobile App"] --> WAF\["WAF"]
Admin\["Admin Portal"] --> GW\["API Gateway"]
WAF --> GW
GW --> Mesh\["Service Mesh"]
Mesh --> Cust\["Customer Domain"]
Mesh --> KYC\["KYC Service"]
Mesh --> Loan\["Loan Service"]
Mesh --> Risk\["Risk Engine"]
Mesh --> Pay\["Payment Service"]
Mesh --> Notif\["Notification Service"]
Cust --> Kafka\["Kafka"]
KYC --> Kafka
Loan --> Kafka
Risk --> Kafka
Pay --> Kafka
Notif --> Kafka
Cust --> DB\["PostgreSQL"]
KYC --> DB
Loan --> DB
Risk --> DB
Pay --> DB
Cust --> Cache\["Redis"]
Pay --> Core\["Core Banking"]
Notif --> Email\["Email/SMS Provider"]
```

\---

# 2\. BUSINESS PROCESS FLOW

!\[Business Process](01\_Project\_Overview/assets/02\_Business\_Process\_Flow.png)

``` mermaid
graph TD
O\["Onboarding"] --> A\["Auth"]
A --> E\["Eligibility"]
E --> L\["Loan Apply"]
L --> R\["Risk Assessment"]
R --> D\["Decision"]
D --> Dis\["Disbursement"]
Dis --> Rep\["Repayment"]
```

\---

# 3\. SCREEN FLOW

!\[Screen Flow](03\_Screen\_Behavior\_UI\_UX/assets/03\_Screen\_Flow.png)

``` mermaid
graph LR
S\["Splash"] --> W\["Welcome"]
W --> Reg\["Register"]
W --> Log\["Login"]
Reg --> OTP\["OTP"]
OTP --> Log
Log --> Dash\["Dashboard"]
Dash --> Sim\["Simulation"]
Sim --> App\["Loan Form"]
App --> Proc\["Processing"]
Proc --> Appr\["Approved"]
Proc --> Rej\["Rejected"]
Appr --> Pay\["Payment"]
Pay --> Res\["Result"]
Dash --> Notif\["Notification Center"]
Dash --> Profile\["Profile"]
```

\---

# 4\. ERD - DATABASE DESIGN

!\[ERD](02\_Architecture\_Design/assets/04\_ERD.png)

``` mermaid
graph TD
U\["USERS"] --> L\["LOANS"]
U --> K\["KYC\_VERIFICATIONS"]
L --> T\["TRANSACTIONS"]
```

\---

# 5\. API DESIGN

!\[API Design](02\_Architecture\_Design/assets/05\_API\_Design.png)

``` mermaid
graph TD
GW\["API Gateway"]
GW --> R\["POST /register"]
GW --> L\["POST /login"]
GW --> K\["POST /kyc"]
GW --> A\["POST /loan/apply"]
GW --> D\["PUT /risk/decision"]
GW --> P\["POST /payments"]
GW --> N\["POST /notify"]
```

\---

# 6\. SEQUENCE DIAGRAM

!\[Sequence Diagram](04\_Sequence\_Diagrams/assets/06\_Sequence\_Diagram.png)

``` mermaid
sequenceDiagram
User ->> Gateway: Apply Loan
Gateway ->> Loan Service: Submit Application
Loan Service ->> Database: Save Data
Loan Service ->> Kafka: Publish Event
Kafka ->> Risk Engine: Risk Evaluation
Risk Engine ->> Kafka: Decision Result
Kafka ->> Notification: Send Result
Notification ->> User: Notification
```

\---

# 7\. STATE MACHINE

!\[State Machine](03\_Screen\_Behavior\_UI\_UX/assets/07\_State\_Machine.png)

``` mermaid
stateDiagram-v2
\[\*] --> Splash
Splash --> Onboarding
Onboarding --> Register
Onboarding --> Login
Register --> OTP
OTP --> Login
Login --> Dashboard
Dashboard --> Simulation
Simulation --> Application
Application --> Processing
Processing --> Approved
Processing --> Rejected
Approved --> Dashboard
Rejected --> Dashboard
```

\---

# 8\. LOW \& HIGH DESIGN

!\[Wireframe](03\_Screen\_Behavior\_UI\_UX/assets/08\_Wireframe\_Design.png)

``` mermaid
graph LR
Splash --> Intro
Intro --> Register
Intro --> Login
Register --> OTP
OTP --> Login
Login --> Dashboard
Dashboard --> Simulation
Simulation --> Application
Application --> Processing
Processing --> Approved
Processing --> Rejected
Approved --> Payment
Payment --> Result
Dashboard --> Notification
Dashboard --> Settings
```

\---

# 9\. TRACEABILITY MATRIX

!\[Traceability](01\_Project\_Overview/assets/09\_Traceability\_Matrix.png)

BR-ID   Requirement   Endpoint             Screen

\---

BR-01   Register      POST /register       Screen 03
BR-02   Login         POST /login          Screen 05
BR-03   KYC           POST /kyc            Screen 08
BR-04   Apply Loan    POST /loan/apply     Screen 13
BR-05   Decision      PUT /risk/decision   Screen 15/16

\---

# 10\. ASSUMPTIONS

!\[Assumptions](01\_Project\_Overview/assets/10\_Assumptions.png)

``` mermaid
graph TD
A\["Key Assumptions"]
A --> B\["Business: Max 12M, 12 Months"]
A --> U\["Users: 18+, Valid Identity"]
A --> S\["System: Microservices, PostgreSQL"]
A --> Sec\["Security: JWT, TLS 1.3"]
```

\---

# 11\. NON-FUNCTIONAL REQUIREMENTS

!\[NFR](02\_Architecture\_Design/assets/11\_NFR.png)

* Availability: 99.9%
* Performance: < 2 Seconds Response
* Scalability: Kubernetes Horizontal Scaling
* Security: OAuth2, JWT, WAF
* Compliance: ISO 27001, OJK

\---

# 

