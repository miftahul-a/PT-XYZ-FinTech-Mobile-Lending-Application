# PT XYZ FinTech - Mobile Lending Application (Solution Analyst Assessment)

> **Tech Stack**: Enterprise Microservices, Cloud Native, Event-Driven (Kafka), PostgreSQL, Kubernetes.

---

## ✅ Mapping Terhadap Soal Technical Test

Berikut adalah daftar jawaban lengkap berdasarkan 4 poin soal tes. Anda dapat melihat **File Gambar (Visual Assets)** yang kami desain, serta **Diagram Kode (Mermaid)** yang dapat di-*render* secara interaktif oleh GitHub.

| Soal Technical Test | Visual Assets (File Gambar PNG) | Alternatif Kode Mermaid |
| :--- | :--- | :--- |
| **1. High Level Design Architecture** | `High_Level_Design_Architecture.png` | Lihat Bagian 1 |
| **2. Screen Flow & ERD** | `Screen_Flow_1.png`, `Screen_Flow_2.png`, `ERD_Database_Design.png` | Lihat Bagian 3 & 4 |
| **3. Detail Design API (UML, ERD, Flowchart)** | `API_DESIGN_ARCHITECTURE_ENDPOINT.png`, `Sequence_Diagram.png` | Lihat Bagian 5 & 6 |
| **4. Detail Screen Behavior (State Machine)** | `State_Machine.png`, `Low_Design_Key_Screens.png`, `High_Design_Key_Screens.png` | Lihat Bagian 7 & 8 |
| **Tambahan: NFR, Traceability, Assumptions** | `Non_Functional_Requirements.png`, `Traceability_Matrix.png`, `Assumptionas.png` | Lihat Bagian 9, 10, 11 |

---

## 📂 1. HIGH LEVEL DESIGN ARCHITECTURE (Jawaban Soal No. 1)
![High Level Architecture](02_Architecture_Design/assets/High_Level_Design_Architecture.png)

**Mermaid Equivalent:**
```mermaid
graph TD
    subgraph Client_Layer
        MobileApp["Mobile App (React Native)"] --> WAF["Cloudflare WAF"]
        AdminPortal["Admin Portal (React.js)"] --> Gateway["API Gateway (Kong/Nginx)"]
    end
    WAF --> Gateway
    Gateway --> ServiceMesh["Service Mesh (Istio)"]
    
    ServiceMesh --> CustSvc["Customer Domain Service"]
    ServiceMesh --> KYCSvc["KYC Verification Service"]
    ServiceMesh --> LoanSvc["Loan Origination Service"]
    ServiceMesh --> RiskSvc["Risk Decision Engine"]
    ServiceMesh --> PaySvc["Payment & Collection Service"]
    ServiceMesh --> NotifSvc["Notification Orchestrator"]

    subgraph Event_Layer
        Kafka["Message Broker (Kafka/RabbitMQ)"]
    end
    CustSvc & KYCSvc & LoanSvc & RiskSvc & PaySvc & NotifSvc --> Kafka
    
    subgraph Data_Layer
        DB["PostgreSQL (Primary DB)"]
        Cache["Redis (Caching Layer)"]
        Storage["Object Storage (S3/MinIO)"]
        ES["ElasticSearch (Logging & Search)"]
    end
    CustSvc & KYCSvc & LoanSvc & RiskSvc & PaySvc & NotifSvc --> DB
    CustSvc & KYCSvc --> Cache
    KYCSvc & NotifSvc --> Storage
    PaySvc --> ES

    subgraph External_Integration
        CoreBank["Core Banking System"]
        PayGateway["Payment Gateway (Midtrans/Xendit)"]
        KYCProvider["KYC Provider (eKYC)"]
        NotifProvider["Email / SMS Provider"]
    end
    PaySvc --> CoreBank
    PaySvc --> PayGateway
    KYCSvc --> KYCProvider
    NotifSvc --> NotifProvider