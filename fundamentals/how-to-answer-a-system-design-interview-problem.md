# **ควรตอบโจทย์/คำถาม System Design Interview อย่างไร?**

การสัมภาษณ์ [**System Design**](https://www.geeksforgeeks.org/system-design/what-is-system-design-learn-system-design/) มีความสำคัญสำหรับตำแหน่ง Software Engineering โดยเฉพาะตำแหน่งระดับ Senior การสัมภาษณ์ลักษณะนี้ใช้ประเมินความสามารถในการออกแบบสถาปัตยกรรมระบบที่รองรับการขยายตัวและมีประสิทธิภาพ ซึ่งแตกต่างจาก Coding Interview ที่จะเน้นการออกแบบโดยรวม การแก้ปัญหา และทักษะการสื่อสาร คุณจำเป็นต้องเข้าใจ Requirements พิจารณา Trade-off อย่างมีเหตุผล และอธิบายเหตุผลของการตัดสินใจให้ได้ บทความนี้นำเสนอเคล็ดลับและแนวทางเชิงปฏิบัติที่จะช่วยให้คุณรับมือกับโจทย์ System Design Interview ได้อย่างมั่นใจ

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240604135139/How-to-Answer-a-System-Design-Interview-Problem-660.webp" alt="How-to-Answer-a-System-Design-Interview-Problem" />

ด้านล่างคือขั้นตอนในการตอบโจทย์ System Design Interview:

**ขั้นตอนสำคัญในการตอบโจทย์ System Design Interview**

- **ขั้นตอนที่ 1: ทำความเข้าใจ Requirements ให้ชัดเจน**
- **ขั้นตอนที่ 2: ประเมิน Capacity**
- **ขั้นตอนที่ 3: High-Level Design**
- **ขั้นตอนที่ 4: Low-Level Design**
- **ขั้นตอนที่ 5: ออกแบบ Database**
- **ขั้นตอนที่ 6: ออกแบบ API**
- **ขั้นตอนที่ 7: องค์ประกอบสำคัญของระบบ**
- **ขั้นตอนที่ 8: ประเด็นปัญหาที่ต้องพิจารณา**
- **โจทย์ฝึกทำ System Design**

## ขั้นตอนที่ 1: ทำความเข้าใจ [Requirements](./what-is-requirements-gathering-process.md) ให้ชัดเจน

### **1. ทำความเข้าใจ Problem Statement**

- **ตั้งใจฟัง:** ต้องแน่ใจว่าคุณเข้าใจความหมายของคำถามที่ถูกถามอย่างถูกต้อง หากไม่เข้าใจคำถาม ควรขอให้ผู้สัมภาษณ์พูดซ้ำหรืออธิบายเพิ่มเติม
- **สรุปปัญหา:** ตรวจสอบว่าคุณเข้าใจสิ่งที่อ่านโดยอ่าน Problem Statement แล้วอธิบายใหม่ด้วยคำพูดของคุณเอง วิธีนี้ช่วยลดความเข้าใจผิดระหว่างคุณกับผู้สัมภาษณ์ได้

### **2. ถามคำถามเพื่อทำความเข้าใจให้ชัดเจน**

**ขอบเขตและข้อจำกัด:**

- **ฐานผู้ใช้:** ประเมินจำนวนผู้ใช้ที่จะใช้งานเว็บไซต์ หรือกล่าวอีกอย่างคือ ระบบนี้เป็น Intranet หรือ Extranet?
- **Scale:** จำนวน Request ต่อวินาทีที่คาดว่าจะเกิดขึ้น ความต้องการด้าน Database และ Throughput
- **Latency และ Performance:** แอปพลิเคชันนี้มีข้อกำหนดด้าน Performance หรือ Latency อย่างไร?

**ฟีเจอร์และ [Functional Requirements](https://www.geeksforgeeks.org/system-design/what-are-functional-requirements-in-system-design-examples-definition/):**

- **ฟังก์ชันหลัก:** ระบบจำเป็นต้องทำงานหลักอะไรบ้าง?
- **ฟีเจอร์เสริม:** มีฟีเจอร์เพิ่มเติมใดที่ผู้ใช้อาจต้องการ แต่ไม่ใช่ฟังก์ชันที่จำเป็นหรือไม่?
- **Use Cases:** ตัวอย่างสถานการณ์ทั่วไปที่ระบบควรรองรับได้

[**Non-Functional Requirements:**](https://www.geeksforgeeks.org/system-design/what-are-non-functional-requirements-in-system-design-examples-definition/)

- [**Availability:**](https://www.geeksforgeeks.org/system-design/availability-in-system-design/) ควรกำหนด SLA (Service Level Agreement) ไว้ที่ระดับใด? ระบบรองรับฟังก์ชันที่มีความสำคัญสูงหรือไม่?
- [**Scalability:**](https://www.geeksforgeeks.org/system-design/what-is-scalability/) ระบบจำเป็นต้องรองรับการเติบโตอย่างรวดเร็วหรือไม่? ต้องการ Elasticity ในระดับใด?
- **Security:** ต้องจัดเตรียมมาตรการด้าน Security แบบใด? มีข้อกำหนดจากหน่วยงานหรือองค์กรที่เกี่ยวข้องหรือไม่?
- [**Maintainability:**](https://www.geeksforgeeks.org/system-design/maintainability-in-system-design/) ระบบควรใช้งานง่ายและสามารถ Upgrade ได้ง่ายในระดับใด?

## ขั้นตอนที่ 2: ประเมิน Capacity

### **1. ประเมิน Traffic**

- **Users:** คาดการณ์จำนวน DAU ที่มีอยู่ในช่วงเวลาหนึ่ง
- **Requests:** ประเมินจำนวน Request ต่อวินาทีในช่วงที่มี Load สูง

### **2. ประเมิน Storage**

- **ปริมาณข้อมูล:** คำนวณว่ามีข้อมูลถูกสร้างขึ้นมากเท่าใดต่อวัน ต่อเดือน และต่อปี
- **การเติบโตของข้อมูล:** ต้องคำนึงถึงอัตราการเติบโตในอนาคตด้วย

### **3. Network Bandwidth**

ประเมินความต้องการ Bandwidth จากข้อมูล เช่น ปริมาณข้อมูลที่รับส่งและ RPS

## ขั้นตอนที่ 3: [High-Level Design](https://www.geeksforgeeks.org/system-design/what-is-high-level-design-learn-system-design/)

### **1. ภาพรวมของสถาปัตยกรรม**

- **Components:** ระบุองค์ประกอบหลัก เช่น Front-end, Back-end, Database, Caching Layer และ Load Balancer
- **Interactions:** ออกแบบ Data Flow หรือ Activity Diagram ในระดับ Logical เพื่อแสดงการสื่อสารระหว่าง Object ต่างๆ

### **2. หลักการออกแบบ**

- **Modularity:** การออกแบบควรประกอบด้วย Component ที่เชื่อมโยงกันแบบ Loose Coupling
- [**Scalability:**](https://www.geeksforgeeks.org/system-design/what-is-scalability/) ควรออกแบบโดยคำนึงถึงการรองรับการเติบโตในอนาคต เช่น การใช้ Load Balancer และ Horizontal Scaling
- [**Reliability:**](https://www.geeksforgeeks.org/system-design/reliability-in-system-design/) เพิ่มองค์ประกอบที่ช่วยเพิ่ม Reliability เช่น Redundancy และ Failover Mechanism

## ขั้นตอนที่ 4: [Low-Level Design](https://www.geeksforgeeks.org/system-design/what-is-low-level-design-or-lld-learn-system-design/)

- **การออกแบบ Component แบบละเอียด:** ออกแบบแต่ละ Component ที่อยู่ใน High-Level Design ให้ละเอียดมากขึ้น แสดง Diagram และอธิบายการทำงานของแต่ละ Component
- **Data Flow:** อธิบายว่าข้อมูลเคลื่อนที่ภายในระบบอย่างไร โดยควรมีรายละเอียดเกี่ยวกับการประมวลผลและการสื่อสารข้อมูลระหว่าง Component

## ขั้นตอนที่ 5: [ออกแบบ Database](https://www.geeksforgeeks.org/system-design/complete-reference-to-databases-in-designing-systems/)

### **1. ออกแบบ Schema**

- **Entities และ Relationships:** ระบุ Entity หลักและความสัมพันธ์ระหว่าง Entity เหล่านั้น
- **Normalization:** ตรวจสอบว่า Database ไม่มีข้อมูลซ้ำซ้อน กล่าวคือ Database Schema ควรถูก Normalize อย่างเหมาะสม

### **2. โซลูชันด้าน Storage**

- **เลือก DBMS ที่เหมาะสม:** เลือกเทคโนโลยี Database ที่เหมาะสม เช่น SQL หรือ NoSQL
- อธิบายโดยใช้เงื่อนไขของ Use Case ว่าเหตุใดจึงเลือกเทคโนโลยีนี้

### **3. Indexes และ Queries**

- สร้าง Index เพื่อเพิ่มประสิทธิภาพในการค้นหา
- ระบุว่าจะทำให้ Query มีประสิทธิภาพและตอบโจทย์ Performance Requirements ได้อย่างไร

## ขั้นตอนที่ 6: ออกแบบ API

- **Endpoints:** ประเมิน Public API Endpoint ที่จำเป็นสำหรับแต่ละฟังก์ชันสำคัญ และบังคับใช้ข้อกำหนดของการออกแบบแบบ RESTful หรือรูปแบบสถาปัตยกรรมอื่นๆ
- **รูปแบบ Request และ Response:** เลือก Media Type และรูปแบบ Request/Response เช่น JSON หรือ XML พร้อมตัวอย่าง Payload
- **Error Handling:** กำหนดนโยบายการจัดการ Error เช่น จะจัดการหรือสื่อสาร Error อย่างไร เช่น ใช้ Standard Error Code

## ขั้นตอนที่ 7: องค์ประกอบสำคัญของระบบ

- **Frontend:**
    - UI/UX: อธิบาย UI และ UX ของผลิตภัณฑ์โดยย่อ
    - Client-Side Logic: อธิบาย Application Logic ฝั่ง Client เช่น SPA และ Mobile App
- **Backend:**
    - Business Logic: อธิบายสิ่งที่เกิดขึ้นฝั่ง Server ของระบบในส่วนของ Business Logic
    - Microservices: หากระบบใช้ Microservices ให้อธิบายโดยย่อว่าคืออะไรและนำมาใช้งานอย่างไร
- **Database:** ดูรายละเอียดของ Schema และ Storage ได้ในส่วนการออกแบบ Database
- **Caching:** อธิบายเทคนิค Caching ต่างๆ ที่ช่วยลด Workload และเพิ่มความเร็วในการตอบสนองของแอปพลิเคชัน เช่น Redis และ Memcached
- **Load Balancer:** อธิบายประโยชน์ของการใช้ Load Balancer เพื่อจัดการ Traffic และ Uptime

## ขั้นตอนที่ 8: ประเด็นปัญหาที่ต้องพิจารณา

### **1. Scalability**

- **Horizontal vs Vertical Scaling:** อธิบายว่าระบบสามารถ Scale ได้อย่างไรด้วยการเพิ่มจำนวนเครื่อง หรือเพิ่มความสามารถของเครื่องที่มีอยู่
- **Load Balancing:** กระจาย Traffic ระหว่าง Node ด้วย Load Balancer
- **Partitioning และ Sharding Components:** อธิบายเทคนิค Partitioning สำหรับ Big Data หรือ Dataset ขนาดใหญ่

### **2. Reliability**

- **Redundancy:** เพิ่มความซ้ำซ้อนในระดับต่างๆ เช่น RAID, การใช้หลาย Instance และ Data Replication
- **Failover Mechanisms:** ออกแบบให้ระบบสามารถฟื้นตัวได้เองเมื่อ Component ใด Component หนึ่งเกิดความผิดปกติ
- **Monitoring และ Alerts:** ใช้เครื่องมือ Monitoring และ Alerting เพื่อให้สามารถตรวจจับและแก้ไขปัญหาได้อย่างทันท่วงที

## **โจทย์ฝึกทำ System Design**

ด้านล่างคือตัวอย่างโจทย์สำหรับฝึก System Design:

- [**System Design | URL Shortener (bit.ly, TinyURL, etc)**](https://www.geeksforgeeks.org/system-design/system-design-url-shortening-service/)
- [**ออกแบบ Restaurant Management System**](https://www.geeksforgeeks.org/system-design/design-restaurant-management-system-system-design/)
- [**System Design Netflix | สถาปัตยกรรมฉบับสมบูรณ์**](https://www.geeksforgeeks.org/system-design/system-design-netflix-a-complete-architecture/)
- [**ออกแบบ Google Maps**](https://www.geeksforgeeks.org/system-design/designing-google-maps-system-design/)
- [**System Design ของแอป Uber**](https://www.geeksforgeeks.org/system-design/system-design-of-uber-app-uber-system-architecture/)
