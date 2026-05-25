---
type: concept
title: Data Engineering Undercurrents
sources: [fundamentals-of-data-engineering]
---

## Definition

**Undercurrents** (กระแสใต้น้ำ) คือ หลักปฏิบัติ 6 ด้านที่วิ่งอยู่ตลอดทุกขั้นตอนของ [[data-engineering-lifecycle]] ขาดอันใดอันหนึ่งแล้วระบบจะไม่สมบูรณ์

---

## Details

### ภาพรวม 6 Undercurrents

```mermaid
mindmap
  root((Undercurrents))
    🔒 Security
      Principle of Least Privilege
      Access control: Data + Systems
      Encryption in-flight and at-rest
      IAM roles & policies
      GDPR / CCPA compliance
    📋 Data Management
      Data Governance
      Data Quality Management
      Metadata Management
      Master Data Management
      Data Lineage
      Data Catalog
    ⚡ DataOps
      Observability & Monitoring
      Alerting
      Incident Reporting
      Pipeline automation
      CI/CD for data
    🏛️ Data Architecture
      Analyze trade-offs
      Design for agility
      Scalability
      Build loosely coupled systems
    🎯 Orchestration
      Coordinate workflows
      Schedule jobs (e.g. Airflow)
      Manage task dependencies
      Handle failures
    💻 Software Engineering
      Production-grade code
      SQL + Python + JVM + bash
      Testing & debugging
      Design patterns
      Code review
```

---

### 1. Security — ความปลอดภัย

> "Security must be top of mind for data engineers, and those who ignore it do so at their peril."

**Principle of Least Privilege**: ให้สิทธิ์แค่ที่จำเป็นสำหรับงาน ไม่มากกว่านั้น

```mermaid
flowchart TD
    A["ผู้ใช้/ระบบ"] --> Q{"ต้องการสิทธิ์อะไร?"}
    Q -->|"แค่ที่จำเป็น"| OK["✅ ให้สิทธิ์เท่าที่ต้องการ"]
    Q -->|"admin ทุกคน"| BAD["❌ Anti-pattern!\nอันตรายมาก"]
```

**ประเภทความปลอดภัย:**
- Access control — ใครเข้าถึงข้อมูลอะไรได้
- Encryption — ทั้ง in-flight (ขณะส่ง) และ at-rest (ขณะเก็บ)
- IAM — Identity and Access Management
- Network security
- Compliance — GDPR, CCPA

---

### 2. Data Management — การจัดการข้อมูล

**DAMA DMBOK** definition:
> "Data management is the development, execution, and supervision of plans, policies, programs, and practices that deliver, control, protect, and enhance the value of data and information assets throughout their lifecycle."

**องค์ประกอบหลัก:**

| องค์ประกอบ | คืออะไร |
|-----------|---------|
| **Data Governance** | นโยบายและมาตรฐานการใช้ข้อมูล |
| **Data Quality** | ความถูกต้อง ครบถ้วน ทันสมัย |
| **Metadata Management** | ข้อมูลเกี่ยวกับข้อมูล (schema, lineage) |
| **Master Data Management** | ข้อมูลอ้างอิงกลาง (customer, product) |
| **Data Lineage** | ติดตามว่าข้อมูลมาจากไหน ผ่านอะไร |
| **Data Catalog** | แค็ตตาล็อกค้นหาข้อมูลในองค์กร |

---

### 3. DataOps — ปฏิบัติการข้อมูล

DataOps ยืมแนวคิดจาก DevOps มาใช้กับ data pipelines:

```mermaid
flowchart LR
    CODE["🔧 Pipeline Code"] --> CI["CI: Test\nauto"]
    CI --> CD["CD: Deploy\nauto"]
    CD --> MON["📊 Monitor\n& Alert"]
    MON -->|"issue detected"| INC["🚨 Incident\nResponse"]
    INC --> CODE
```

**เป้าหมาย DataOps:**
- Observability — มองเห็นได้ว่า pipeline ทำงานอย่างไร
- เตือนเมื่อมีปัญหา
- ลด time-to-detect และ time-to-resolve

---

### 4. Data Architecture — สถาปัตยกรรมข้อมูล

**9 Principles of Good Data Architecture** (จาก Ch. 3):
1. Choose common components wisely
2. Plan for failure
3. Architect for scalability
4. Architecture is leadership
5. Always be architecting
6. Build loosely coupled systems
7. Make reversible decisions
8. Prioritize security
9. Embrace FinOps

**Architecture patterns ที่สำคัญ:**

```mermaid
flowchart TD
    A["Architecture Patterns"] --> DWH["Data Warehouse\nstructured, SQL, analytics"]
    A --> DL["Data Lake\nschema-on-read, flexible"]
    A --> DLH["Data Lakehouse\nDL + DWH combined"]
    A --> LMBD["Lambda Architecture\nBatch + Streaming layers"]
    A --> KPPA["Kappa Architecture\nStreaming-only"]
    A --> DM["Data Mesh\nDomain-oriented, decentralized"]
```

---

### 5. Orchestration — การประสานงาน

Orchestration = "ผู้ควบคุมวง" ของ data pipelines

```mermaid
flowchart TD
    ORCH["🎯 Orchestrator\n(e.g. Airflow)"]
    ORCH --> T1["Task 1: Extract"]
    T1 --> T2["Task 2: Transform"]
    T2 --> T3["Task 3: Load"]
    T2 --> T4["Task 4: Quality Check"]
    T4 --> T5["Task 5: Notify"]
    ORCH -->|"schedule"| CRON["⏰ ทุกวัน 2:00 AM"]
    ORCH -->|"retry on fail"| RETRY["🔄 Retry 3 times"]
```

---

### 6. Software Engineering — การพัฒนาซอฟต์แวร์

ภาษาที่ Data Engineer ต้องรู้:

| ภาษา | ใช้ทำอะไร |
|-----|----------|
| **SQL** | lingua franca ของ data, analytics, transformation |
| **Python** | glue language, Airflow, pandas, PySpark |
| **JVM (Java/Scala)** | Apache Spark, Flink, Hive |
| **bash** | scripting, CLI operations, automation |

---

## Related

- [[data-engineering-lifecycle]] — lifecycle ที่ undercurrents รองรับ
- [[fundamentals-of-data-engineering]] — source
- [[data-maturity-model]] — undercurrents ซับซ้อนขึ้นตาม maturity
