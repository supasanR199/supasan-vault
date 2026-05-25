---
type: concept
title: Data Engineering Lifecycle
sources: [fundamentals-of-data-engineering]
---

## Definition

**Data Engineering Lifecycle** คือ กรอบงาน (framework) ที่อธิบายเส้นทางการเดินทางของข้อมูลตั้งแต่ต้นทาง (source) จนถึงปลายทาง (serving) โดยมี 5 ขั้นตอนหลักและ undercurrents ที่วิ่งตลอด

> แนวคิดนี้ช่วยให้ Data Engineer มองภาพรวมงานตัวเองแทนที่จะมุ่งแต่ technology

---

## Details

### 5 ขั้นตอนหลัก

```mermaid
flowchart TD
    subgraph main["Data Engineering Lifecycle"]
        G["🌱 Generation\nSource Systems\n(DB, IoT, API, แอป)"]
        I["📥 Ingestion\nดึงข้อมูลจาก source\n(Batch / Streaming)"]
        T["🔀 Transformation\nแปลง raw → useful\n(ETL/ELT, modeling)"]
        SV["📤 Serving\nส่งให้ผู้ใช้ปลายทาง"]
        ST["💾 Storage\nรองรับทุกขั้นตอน"]

        G --> I --> T --> SV
        ST -.->|"foundation"| I
        ST -.-> T
        ST -.-> SV
    end

    SV --> A["📊 Analytics\n(BI, Operational, Embedded)"]
    SV --> ML["🤖 Machine Learning"]
    SV --> R["🔁 Reverse ETL\n(ส่งกลับ source systems)"]
```

### Undercurrents

ส่วนที่วิ่งอยู่ตลอดทุกขั้นตอน — ขาดอันใดอันหนึ่งไม่ได้:

| Undercurrent | หน้าที่ |
|-------------|---------|
| **Security** | ควบคุมการเข้าถึง, encryption, least privilege |
| **Data Management** | governance, quality, metadata, lineage |
| **DataOps** | observability, monitoring, incident response |
| **Data Architecture** | trade-off analysis, design for agility |
| **Orchestration** | schedule jobs, coordinate workflows |
| **Software Engineering** | coding, testing, design patterns |

### Lifecycle vs Full Data Lifecycle

```mermaid
flowchart TD
    FDL["Full Data Lifecycle\n(ครอบคลุมตลอดอายุข้อมูล)"]
    FDL --> DEL["Data Engineering Lifecycle\n(ส่วนที่ DE ควบคุม)"]
    style FDL fill:#e0e0e0
    style DEL fill:#4a90d9,color:#fff
```

---

## Examples

**ตัวอย่าง E-commerce Pipeline:**

```mermaid
flowchart LR
    S1["🛒 Order DB\n(OLTP)"] --> I["Ingestion\nCDC / batch"]
    S2["📱 Mobile App\n(events)"] --> I
    I --> ST["☁️ Cloud Storage\n(S3/GCS)"]
    ST --> T["Transform\n(dbt / Spark)"]
    T --> DWH["🏛️ Data Warehouse"]
    DWH --> BI["📊 Dashboard\n(Tableau)"]
    DWH --> ML["🤖 Recommendation\nModel"]
    DWH --> RE["🔁 Reverse ETL\n→ CRM/Ads"]
```

---

## Related

- [[fundamentals-of-data-engineering]] — source
- [[data-engineering-undercurrents]] — รายละเอียด undercurrents
- [[data-maturity-model]] — ระดับ maturity องค์กร
- [[data-loading-patterns]] — ingestion patterns
