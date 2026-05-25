---
type: source
title: "Fundamentals of Data Engineering: Plan and Build Robust Data Systems"
date_ingested: 2026-05-25
source_file: "raw/Fundamentals of Data Engineering (Reis, JoeHousley, Matt) (Z-Library).pdf"
authors: Joe Reis & Matt Housley
publisher: O'Reilly Media, 2022
---

## Summary

หนังสือเล่มนี้เป็น **คู่มือหลัก** ของวิชา Data Engineering ที่ไม่ยึดติดกับ tool ใดเครื่องมือหนึ่ง แต่สอน **หลักคิด (principles)** ที่คงทนต่อเวลา แกนกลางของหนังสือคือ **Data Engineering Lifecycle** — กรอบงานที่ช่วยให้วิศวกรข้อมูลมองภาพรวมของงานตัวเองได้ครบ

> ผู้เขียนเปรียบตัวเองว่าเป็น "recovering data scientists" — เคยทำ Data Science แต่ติดปัญหาเรื่อง infrastructure จึงหันมาสนใจ Data Engineering อย่างจริงจัง

The book is organized into three parts:
- **Part I** — Foundation & Building Blocks (Ch.1–4): definitions, lifecycle, architecture, tech selection
- **Part II** — Lifecycle in Depth (Ch.5–9): each stage has its own chapter
- **Part III** — Security, Privacy & Future (Ch.10–11)

---

## Key Concepts

### 1. What Is Data Engineering?

**Data engineering** คือ การพัฒนา ดูแล และบำรุงรักษาระบบและกระบวนการ ที่รับข้อมูลดิบ (raw data) แล้วผลิตข้อมูลคุณภาพสูงออกมาเพื่อ use cases ปลายทาง เช่น analytics และ machine learning

> *"Data engineering is the development, implementation, and maintenance of systems and processes that take in raw data and produce high-quality, consistent information that supports downstream use cases."*

**Data Engineer คือ** คนที่จัดการ Data Engineering Lifecycle ตั้งแต่รับข้อมูลจาก source systems จนถึงส่งข้อมูลให้ใช้งาน

Data Engineering อยู่ **upstream** จาก Data Science:

```mermaid
flowchart LR
    A["📦 Data Sources\nแหล่งข้อมูล"] --> B["⚙️ Data Engineering\n(upstream)"]
    B --> C["🔬 Data Science & Analytics\n(downstream)"]
    style B fill:#4a90d9,color:#fff
    style C fill:#f5a623,color:#fff
```

---

### 2. The Data Engineering Lifecycle

**วงจรชีวิตของ Data Engineering** — หัวใจหลักของหนังสือ มี 5 ขั้นตอน:

```mermaid
flowchart LR
    subgraph lifecycle["🔄 Data Engineering Lifecycle"]
        direction LR
        G["🌱 Generation\nสร้างข้อมูล"] --> I["📥 Ingestion\nนำข้อมูลเข้า"]
        I --> T["🔀 Transformation\nแปลงข้อมูล"]
        T --> S["📤 Serving\nส่งข้อมูล"]
        ST["💾 Storage\nจัดเก็บ"] -.->|รองรับทุกขั้น| I
        ST -.-> T
        ST -.-> S
    end

    S --> AN["📊 Analytics"]
    S --> ML["🤖 Machine Learning"]
    S --> RE["🔁 Reverse ETL"]

    subgraph undercurrents["🌊 Undercurrents (กระแสใต้น้ำ)"]
        direction LR
        SEC["🔒 Security"] --- DM["📋 Data Mgmt"]
        DM --- DO["⚡ DataOps"]
        DO --- DA["🏛️ Data Architecture"]
        DA --- OR["🎯 Orchestration"]
        OR --- SE["💻 Software Eng"]
    end

    style lifecycle fill:#e8f4f8
    style undercurrents fill:#fff3e0
```

**อธิบายแต่ละขั้น:**

| Stage | ภาษาไทย | คำอธิบาย |
|-------|---------|----------|
| **Generation** | สร้างข้อมูล | Source systems — DB, IoT, API, แอป |
| **Storage** | จัดเก็บ | รองรับทุกขั้นตอน ตลอด lifecycle |
| **Ingestion** | นำข้อมูลเข้า | ดึงข้อมูลจาก source เข้าสู่ระบบ |
| **Transformation** | แปลงข้อมูล | เปลี่ยน raw → ข้อมูลที่มีประโยชน์ |
| **Serving** | ส่งข้อมูล | ส่งให้ analytics, ML, Reverse ETL |

> ⚠️ **สิ่งสำคัญ:** Storage ไม่ใช่แค่ขั้นตอนหนึ่ง — มันรองรับทุกขั้น ข้อมูลผ่านการจัดเก็บตลอดเส้นทาง

---

### 3. Undercurrents — กระแสใต้น้ำ

สิ่งที่วิ่งอยู่ใต้ทุกขั้นตอนของ lifecycle ขาดไม่ได้:

```mermaid
mindmap
  root((Undercurrents))
    Security
      Access control ข้อมูลและระบบ
      Principle of Least Privilege
      Encryption ทั้ง in-flight และ at-rest
    Data Management
      Data Governance
      Data Quality
      Metadata Management
      Master Data Management
    DataOps
      Observability & Monitoring
      Incident Reporting
      Automation
    Data Architecture
      Analyze trade-offs
      Design for agility
      Add business value
    Orchestration
      Coordinate workflows
      Schedule jobs
      Manage tasks
    Software Engineering
      Coding skills
      Design patterns
      Testing & Debugging
```

---

### 4. Generation — Source Systems

**Source System** = แหล่งกำเนิดข้อมูล เช่น:
- Application databases (OLTP)
- IoT devices / sensors
- Message queues
- SaaS platforms
- Files และ APIs

**คำถามที่ต้องถามเกี่ยวกับ Source System:**

```mermaid
flowchart TD
    Q["🤔 ประเมิน Source System"] --> Q1["ข้อมูลสร้างอย่างไร?\nบ่อยแค่ไหน?"]
    Q --> Q2["Schema คืออะไร?\nFixed หรือ Schemaless?"]
    Q --> Q3["ข้อมูลมี late arrival ไหม?"]
    Q --> Q4["มี duplicates ไหม?"]
    Q --> Q5["อ่านจาก source แล้วกระทบ performance ไหม?"]
    Q --> Q6["มี CDC (Change Data Capture) ไหม?"]
```

---

### 5. Storage — การจัดเก็บข้อมูล

**Data Temperature** — อุณหภูมิของข้อมูล บอกความถี่ในการเข้าถึง:

```mermaid
flowchart LR
    H["🔥 Hot Data\nข้อมูลร้อน\nเข้าถึงบ่อยมาก\n(วินาที/ชั่วโมง)"]
    W["🌡️ Warm Data\nข้อมูลอุ่น\nเข้าถึงเป็นระยะ\n(สัปดาห์/เดือน)"]
    C["❄️ Cold Data\nข้อมูลเย็น\nเข้าถึงน้อย\n(เก็บ archive)"]

    H -->|"ลดความถี่"| W -->|"ลดความถี่"| C
    style H fill:#ff6b6b,color:#fff
    style W fill:#ffa07a,color:#fff
    style C fill:#87ceeb,color:#fff
```

**ประเภท Storage Abstractions:**

| ประเภท | คืออะไร |
|--------|---------|
| **Data Warehouse** | ข้อมูล structured สำหรับ analytics, schema บังคับ |
| **Data Lake** | เก็บทุกรูปแบบ, schema-on-read, ยืดหยุ่น |
| **Data Lakehouse** | ผสม Lake + Warehouse |
| **Data Platform** | ครบวงจร, ทั้ง storage + compute + governance |

---

### 6. Ingestion — การนำข้อมูลเข้า

**Batch vs Streaming:**

```mermaid
flowchart TD
    D["📊 Data (ข้อมูล)"] --> Q{"วิธีนำเข้า?"}

    Q --> B["📦 Batch Ingestion\nนำเข้าเป็นชุด"]
    Q --> S["🌊 Streaming Ingestion\nนำเข้าต่อเนื่อง real-time"]

    B --> B1["✅ เหมาะกับ: รายงานรายวัน\nModel training รายสัปดาห์"]
    B --> B2["⚠️ latency สูง (รอรอบ batch)"]

    S --> S1["✅ เหมาะกับ: fraud detection\nReal-time dashboards"]
    S --> S2["⚠️ ซับซ้อนกว่า ค่าใช้จ่ายสูงกว่า"]

    style B fill:#c8e6c9
    style S fill:#b3d9ff
```

**Push vs Pull:**

| Pattern | คืออะไร | ตัวอย่าง |
|---------|---------|---------|
| **Push** | Source ส่งข้อมูลมาให้เรา | CDC log-based, Webhook |
| **Pull** | เราไปดึงข้อมูลจาก source | ETL extract, REST API polling |

---

### 7. Transformation — การแปลงข้อมูล

**ETL vs ELT:**

```mermaid
flowchart LR
    subgraph etl["🔄 ETL (Extract → Transform → Load)"]
        direction LR
        E1["Extract"] --> T1["Transform\n(ก่อนโหลด)"] --> L1["Load\nto DWH"]
    end

    subgraph elt["⚡ ELT (Extract → Load → Transform)"]
        direction LR
        E2["Extract"] --> L2["Load\nto DWH"] --> T2["Transform\n(ใน DWH)"]
    end

    style etl fill:#e8f4f8
    style elt fill:#fff3e0
```

**Transformation ทำอะไรบ้าง:**
- แปลง data types (string → date, number)
- ทำ normalization / denormalization
- Business logic — "sale = someone bought X for $Y"
- Feature engineering สำหรับ ML
- Data cleaning และ deduplication

---

### 8. Serving Data — การส่งข้อมูล

**3 ประเภทของ Analytics:**

```mermaid
flowchart TD
    AN["📊 Analytics"] --> BI["Business Intelligence\nเข้าใจอดีต-ปัจจุบัน\nรายงาน, Dashboard\n(Tableau, Looker, Power BI)"]
    AN --> OP["Operational Analytics\nreal-time operations\nสต็อก, ระบบ live"]
    AN --> EM["Embedded Analytics\nฝังใน product ให้ลูกค้า\nต้องการ multi-tenancy"]
```

**Reverse ETL** — ส่งข้อมูลกลับสู่ source systems:

```mermaid
flowchart LR
    DWH["🏛️ Data Warehouse\n(ข้อมูลที่แปลงแล้ว)"] -->|"Reverse ETL"| CRM["CRM System"]
    DWH --> ADS["Google Ads"]
    DWH --> SaaS["SaaS Platforms"]
```

> ตัวอย่าง: คำนวณ bid ใน data warehouse แล้วส่งกลับไปที่ Google Ads โดยอัตโนมัติ

---

### 9. Data Maturity Model — ระดับความสุกของข้อมูลในองค์กร

```mermaid
flowchart LR
    S1["Stage 1\n🌱 Starting with Data\nเริ่มต้น\n- ad hoc requests\n- generalist DE\n- สร้าง foundation"]
    S2["Stage 2\n📈 Scaling with Data\nขยาย\n- formal practices\n- specialist roles\n- DevOps/DataOps"]
    S3["Stage 3\n🏆 Leading with Data\nนำด้วยข้อมูล\n- self-service analytics\n- automation\n- data governance"]

    S1 -->|"มี formal practices"| S2
    S2 -->|"data-driven culture"| S3

    style S1 fill:#c8e6c9
    style S2 fill:#b3d9ff
    style S3 fill:#f5c842,color:#333
```

**คำแนะนำในแต่ละ Stage:**

| Stage | หลีกเลี่ยง | ควรทำ |
|-------|-----------|-------|
| Stage 1 | กระโดดไป ML เร็วเกินไป | สร้าง data foundation ก่อน |
| Stage 2 | ใช้ bleeding-edge tech ตาม hype | เลือก tech ที่ deliver value จริง |
| Stage 3 | ทำ vanity projects | รักษา maintenance + governance |

---

### 10. Type A vs Type B Data Engineers

```mermaid
flowchart LR
    DE["Data Engineers"] --> A["Type A\n(Abstraction)\n- ใช้ off-the-shelf tools\n- managed services\n- ทุก industry ทุก stage"]
    DE --> B["Type B\n(Build)\n- สร้าง custom tools\n- competitive advantage\n- Stage 2-3 companies"]
```

---

### 11. Data Engineer ทำงานกับใคร?

```mermaid
flowchart LR
    subgraph up["⬆️ Upstream Producers"]
        SA["Software Engineers"]
        AR["Data Architects"]
        OPS["DevOps / SREs"]
    end

    DE["⚙️ Data Engineer"]

    subgraph down["⬇️ Downstream Consumers"]
        AN["Data Analysts"]
        DS["Data Scientists"]
        ML["ML Engineers"]
    end

    up --> DE --> down
```

**ผู้บริหารที่ DE ทำงานด้วย:**
- **CIO** — IT strategy, data culture
- **CTO** — tech strategy, external systems
- **CDO** — data assets & strategy
- **CAO** — analytics & decision-making

---

## Notes / Observations

- หนังสือเน้น **cloud-first approach** — ถือว่า infrastructure เป็น ephemeral และ scalable
- **"What's old is new again"** — pattern เก่าๆ (data governance, data management) กลับมาใหม่ในยุค modern data stack
- Data Science Hierarchy of Needs: **70-80% ของเวลา data scientist ใช้ไปกับ bottom 3 layers** (collect, move/store, explore/transform) — นี่คืองานของ Data Engineer
- ภาษาหลักที่ DE ต้องรู้: **SQL, Python, JVM (Java/Scala), bash**
- SQL ยังคงสำคัญมาก — "The Unreasonable Effectiveness of SQL"
- **คำเตือน:** อย่าสร้าง "vanity data projects" — เก็บข้อมูลเยอะแต่ไม่มีใครใช้ ข้อมูลที่ไม่ถูก consume คือ "inert" ไม่มีคุณค่า
- Orchestration tools เช่น **Apache Airflow** ถูกพูดถึงบ่อย

---

## Related Concepts

- [[data-engineering-lifecycle]] — รายละเอียดเต็มของ lifecycle
- [[data-engineering-undercurrents]] — Security, DataOps, Orchestration
- [[data-maturity-model]] — 3 stages model
- [[data-loading-patterns]] — เชื่อมกับ ingestion patterns จาก Day 1
- [[pipeline-spec-framework]] — การออกแบบ pipeline จาก Day 1
