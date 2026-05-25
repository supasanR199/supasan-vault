---
type: concept
title: Data Maturity Model
sources: [fundamentals-of-data-engineering]
---

## Definition

**Data Maturity** = ระดับความก้าวหน้าในการใช้ข้อมูลขององค์กร ไม่ได้วัดจากอายุหรือรายได้ แต่วัดจาก **วิธีที่องค์กรใช้ข้อมูลเป็น competitive advantage**

---

## Details

### 3 ระดับของ Data Maturity

```mermaid
flowchart LR
    S1["🌱 Stage 1\nStarting with Data\n\n- ad hoc requests\n- Data Engineer เป็น generalist\n- สร้าง foundation\n- ทีมเล็ก (single digits)"]
    S2["📈 Stage 2\nScaling with Data\n\n- formal data practices\n- เริ่มมี specialist roles\n- DevOps + DataOps\n- scalable architecture"]
    S3["🏆 Stage 3\nLeading with Data\n\n- data-driven culture\n- self-service analytics\n- automation ทุกด้าน\n- data governance เต็มรูป"]

    S1 -->|"มี formal processes\nad hoc ลดลง"| S2
    S2 -->|"automated pipelines\nself-service"| S3

    style S1 fill:#c8e6c9,color:#1b5e20
    style S2 fill:#b3d9ff,color:#0d47a1
    style S3 fill:#f5c842,color:#333
```

---

### Stage 1: Starting with Data

**บริบท:** องค์กรเพิ่งเริ่มต้นกับข้อมูล เป้าหมายยังไม่ชัด

**สิ่งที่ DE ควรทำ:**
- Get buy-in จาก executive (ต้องมี sponsor)
- Define data architecture (มักทำคนเดียว ไม่มี Data Architect แยก)
- สร้าง solid data foundation — อย่ารีบ ML
- Quick wins เพื่อให้องค์กรเห็นคุณค่าของข้อมูล

**⚠️ Pitfalls:**
```mermaid
flowchart TD
    P1["❌ กระโดดไป ML/AI เร็วเกินไป\n→ ไม่มี foundation รองรับ"]
    P2["❌ ทำงานใน silo\n→ ไม่รู้ว่า business ต้องการอะไร"]
    P3["❌ Undifferentiated heavy lifting\n→ สร้าง custom เกินจำเป็น"]
    P4["❌ สะสม technical debt\n→ ทำ quick win แต่ไม่มี plan ชำระหนี้"]
```

---

### Stage 2: Scaling with Data

**บริบท:** มี formal data practices แล้ว กำลังขยายสู่ data-driven organization

**สิ่งที่ DE ควรทำ:**
- Establish formal data practices
- Create scalable and robust architectures
- Adopt DevOps and DataOps practices
- Build systems that support ML
- Roles เริ่มแยกเป็น specialist

**⚠️ Pitfalls:**
- อย่าตามกระแส Silicon Valley — เลือก tech ที่ deliver value จริง
- Bottleneck อยู่ที่ **ทีม** ไม่ใช่ tech
- อย่าทำตัวเป็น "data genius" — สอนองค์กรให้ใช้ข้อมูลด้วย

---

### Stage 3: Leading with Data

**บริบท:** องค์กร data-driven อย่างเต็มตัว ทุกทีมใช้ข้อมูลเป็นรูทีน

**สิ่งที่ DE ควรทำ:**
- Automation สำหรับ data introduction
- Custom tools ที่เป็น competitive advantage
- Data governance + quality + DataOps เต็มรูปแบบ
- Data catalog, lineage tools, metadata systems
- สร้าง community ที่ทุกคนพูดเรื่อง data ได้

**⚠️ Pitfalls:**
- **Complacency** — ถึง stage 3 แล้วนิ่งนอนใจ → ตกกลับไป stage ต่ำได้
- Expensive "hobby projects" ที่ไม่ deliver business value

---

### DE Role เปลี่ยนตาม Maturity

| Stage | DE เป็นอะไร | Focus หลัก |
|-------|-----------|-----------|
| 1 | Generalist | Move fast, สร้าง foundation |
| 2 | Specialist | Scalability, formal practices |
| 3 | Deep specialist | Automation, governance, competitive tools |

---

## Examples

- Startup ที่เพิ่งตั้ง = Stage 1 (แม้อายุน้อยก็ได้)
- บริษัทร้อยปีที่ยังทำ ad hoc Excel = Stage 1
- Netflix, Uber, Airbnb = Stage 3

---

## Related

- [[data-engineering-lifecycle]] — lifecycle ที่ซับซ้อนขึ้นตาม maturity
- [[data-engineering-undercurrents]] — undercurrents ต้องการมากขึ้นใน Stage 2-3
- [[fundamentals-of-data-engineering]] — source
