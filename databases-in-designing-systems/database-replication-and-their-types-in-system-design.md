# **Database Replication ในการออกแบบระบบ**

การทำ Database Replication คือการสร้างและเก็บสำเนาของฐานข้อมูลไว้บนเซิร์ฟเวอร์อื่น ซึ่งเป็นสิ่งสำคัญต่อการเพิ่ม [**ความสามารถในการรองรับการขยายตัว**](https://www.geeksforgeeks.org/system-design/what-is-scalability/), [**ความน่าเชื่อถือ**](https://www.geeksforgeeks.org/system-design/reliability-in-system-design/) และ [**ความพร้อมใช้งานของข้อมูล**](https://www.geeksforgeeks.org/system-design/availability-in-system-design/) ในระบบสมัยใหม่

- การกระจายข้อมูลไปยังหลายเซิร์ฟเวอร์ช่วยให้องค์กรมั่นใจได้ว่าข้อมูลจะยังคงเข้าถึงได้ แม้เซิร์ฟเวอร์เครื่องหนึ่งจะล้มเหลว
- การมีข้อมูลสำรองหลายชุดยังช่วยเพิ่มความน่าเชื่อถือของข้อมูล เพราะสามารถใช้สำเนาเหล่านั้นเพื่อกู้คืนข้อมูลได้ในกรณีที่ข้อมูลเสียหายหรือสูญหาย
- Database Replication ยังช่วยกระจายภาระงานระหว่างเซิร์ฟเวอร์ ทำให้ระบบรองรับการขยายตัวและมีประสิทธิภาพดีขึ้น

> ***ตัวอย่าง:** เว็บไซต์ E-commerce อาจใช้ฐานข้อมูลหลักสำหรับการเขียนข้อมูล และใช้ฐานข้อมูล Replica หลายชุดเพื่อรองรับคำขออ่านข้อมูลจากผู้ใช้*

## **การทำงาน**

ขั้นตอนต่อไปนี้อธิบายการทำงานของ Database Replication:

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260113174041816289/server.webp" alt="การทำงานของ Database Replication" />

1. **กำหนดฐานข้อมูลหลัก (Source)**: เลือกฐานข้อมูลหลัก (Master) ให้เป็นแหล่งข้อมูลหลักที่การเปลี่ยนแปลงข้อมูลทั้งหมดเริ่มต้นขึ้น
2. **ตั้งค่าฐานข้อมูล Replica (Targets)**: กำหนดค่าฐานข้อมูล Replica หนึ่งชุดหรือหลายชุดเพื่อรับข้อมูลจากฐานข้อมูลหลัก
3. **บันทึกการเปลี่ยนแปลงของข้อมูล**: การ Insert, Update และ Delete ทั้งหมดจะถูกบันทึกผ่าน Log หรือกลไก Change Data Capture
4. **ส่งการเปลี่ยนแปลงไปยัง Replica**: การเปลี่ยนแปลงที่บันทึกไว้จะถูกส่งไปยังฐานข้อมูล Replica แบบ Real-time หรือตามช่วงเวลาที่กำหนด
5. **นำการเปลี่ยนแปลงไปใช้กับ Replica**: ฐานข้อมูล Replica จะนำข้อมูลอัปเดตที่ได้รับไปใช้เพื่อให้ข้อมูลสอดคล้องกับฐานข้อมูลหลัก
6. **ตรวจสอบการ Synchronization**: ระบบจะตรวจสอบสถานะของ Replication อย่างต่อเนื่อง และจัดการกับความล่าช้าหรือปัญหาในการ Synchronization
7. **จัดการการอ่าน/เขียนข้อมูล**: การอ่านข้อมูลจะถูกกระจายไปยัง Replica ขณะที่การเขียนข้อมูลโดยทั่วไปจะส่งไปยังฐานข้อมูลหลัก ทั้งนี้ขึ้นอยู่กับรูปแบบที่ใช้งาน

## **ประเภทของ Database Replication**

ทำความเข้าใจ [ประเภทต่างๆ ของ Database Replication](https://www.geeksforgeeks.org/system-design/types-of-database-replication-system-design/):

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260113170807014546/types_of_database_replication-660.webp" />

### **1. Master-Slave Replication**

ในรูปแบบ Replication นี้ ฐานข้อมูลหนึ่งชุดทำหน้าที่เป็นเซิร์ฟเวอร์หลัก ขณะที่ฐานข้อมูลชุดอื่นเก็บสำเนาข้อมูลจากฐานข้อมูลหลัก

- ฐานข้อมูล Master จะจัดการการเขียนข้อมูลทั้งหมด เช่น Insert, Update และ Delete
- ฐานข้อมูล Slave จะทำ Replication ข้อมูลจาก Master และโดยทั่วไปจะใช้สำหรับการอ่านข้อมูล

### **2. Master-Master Replication / Multi-Master Replication**

ในรูปแบบนี้ ฐานข้อมูลหลายชุดทำหน้าที่เป็น Master และสามารถรองรับได้ทั้งการอ่านและการเขียนข้อมูล

- การเปลี่ยนแปลงที่เกิดขึ้นในฐานข้อมูล Master ชุดหนึ่งจะถูกทำ Replication ไปยังฐานข้อมูล Master ชุดอื่น
- ช่วยเพิ่มความพร้อมใช้งานและรองรับการเขียนข้อมูลแบบกระจายไปยังหลายเซิร์ฟเวอร์

### **3. Snapshot Replication**

วิธีนี้ทำ Replication ฐานข้อมูลทั้งหมดด้วยการสร้าง Snapshot ณ ช่วงเวลาหนึ่ง

- ระบบจะสร้างสำเนาฐานข้อมูลทั้งหมดและส่งไปยังเซิร์ฟเวอร์อื่น
- เหมาะสำหรับระบบที่ข้อมูลไม่ได้เปลี่ยนแปลงบ่อยมาก

### **4. Transactional Replication**

Transactional Replication ทำให้ฐานข้อมูลสอดคล้องกันด้วยการทำ Replication การเปลี่ยนแปลงทันทีที่เกิดขึ้น

- การเปลี่ยนแปลงที่เกิดขึ้นในฐานข้อมูล Publisher จะถูกส่งไปยังฐานข้อมูล Subscriber อย่างรวดเร็ว
- ช่วยให้ข้อมูลระหว่างฐานข้อมูลหลายชุดมีความสอดคล้องกันในระดับใกล้เคียง Real-time

### **5. Merge Replication**

Merge Replication ช่วยให้ฐานข้อมูลหลายชุดสามารถอัปเดตข้อมูลแยกจากกันได้ แล้วจึง Synchronize การเปลี่ยนแปลงเข้าด้วยกันในภายหลัง

- ทั้งฐานข้อมูล Publisher และ Subscriber สามารถแก้ไขข้อมูลได้
- ระบบจะตรวจจับและแก้ไข Conflict ระหว่างกระบวนการ Synchronization

## **กลยุทธ์**

[กลยุทธ์ของ Database Replication](https://www.geeksforgeeks.org/system-design/strategies-of-database-replication-system-design/) กำหนดวิธีเลือก คัดลอก และกระจายข้อมูลระหว่างฐานข้อมูล เพื่อให้บรรลุเป้าหมายที่ต้องการ เช่น ความสามารถในการรองรับการขยายตัว ความพร้อมใช้งาน และประสิทธิภาพ

กลยุทธ์ Database Replication ที่ใช้กันทั่วไปมีดังต่อไปนี้:

- **Full Replication:** เรียกอีกอย่างว่า Full Database Replication เป็นเทคนิคที่ทำ Replication ฐานข้อมูลทั้งหมดไปยังเซิร์ฟเวอร์ปลายทางหนึ่งเครื่องหรือหลายเครื่อง โดยตาราง แถว และคอลัมน์ทั้งหมดในฐานข้อมูลจะถูกคัดลอกไปยังเซิร์ฟเวอร์ปลายทาง ทำให้ Replica มีสำเนาที่ตรงกับฐานข้อมูลต้นฉบับ
- **Partial Replication:** วิธีนี้ไม่ได้ทำ Replication ฐานข้อมูลทั้งหมด แต่ทำเฉพาะบางส่วน เช่น ตาราง แถว หรือคอลัมน์ที่กำหนด วิธีนี้มีประโยชน์เมื่อจำเป็นต้องทำสำเนาเฉพาะข้อมูลบางส่วนสำหรับการทำรายงาน การวิเคราะห์ หรือวัตถุประสงค์อื่น และช่วยให้ใช้ทรัพยากรได้อย่างมีประสิทธิภาพมากขึ้น
- **Selective Replication:** เป็นกลยุทธ์ Database Replication ที่ทำ Replication ข้อมูลตามเกณฑ์หรือเงื่อนไขที่กำหนดไว้ล่วงหน้า ต่างจาก Full Replication ที่ทำ Replication ทั้งฐานข้อมูล หรือ Partial Replication ที่ทำเฉพาะบางส่วน Selective Replication ช่วยให้ควบคุมได้ละเอียดมากขึ้นว่าข้อมูลใดจะถูกทำ Replication
- **Sharding:** เป็นเทคนิคสำหรับขยายฐานข้อมูลโดยแบ่งข้อมูลไปยังฐานข้อมูลหลาย Instance (Shard) ตาม Key วิธีนี้ช่วยกระจายภาระงานและพื้นที่จัดเก็บข้อมูลไปยังหลายเซิร์ฟเวอร์ ทำให้ระบบรองรับการขยายตัวและมีประสิทธิภาพดีขึ้น
- **Hybrid Replication:** เป็นกลยุทธ์ Database Replication ที่ผสมผสานเทคนิค Replication หลายรูปแบบเพื่อให้บรรลุเป้าหมายที่ต้องการ วิธีนี้ช่วยให้สามารถปรับแต่งวิธีการ Replication ให้เหมาะกับความต้องการของส่วนต่างๆ ของฐานข้อมูลหรือแอปพลิเคชันได้

## **รูปแบบการกำหนดค่า**

Database Replication สามารถตั้งค่าและทำงานได้หลายรูปแบบ เพื่อให้บรรลุเป้าหมายที่เกี่ยวข้องกับความสอดคล้องของข้อมูล ความพร้อมใช้งาน และประสิทธิภาพ:

### **1. Synchronous Replication Configuration**

ในการทำ Synchronous Replication การเปลี่ยนแปลงข้อมูลจะถูกทำ Replication ไปยัง Replica ทันทีก่อนที่ Transaction จะเสร็จสมบูรณ์

- Transaction จะถูก Commit หลังจากมี Replica อย่างน้อยหนึ่งชุดยืนยันว่าได้รับข้อมูลอัปเดตแล้วเท่านั้น
- ช่วยให้ข้อมูลมีความสอดคล้องกันสูง เพราะฐานข้อมูลหลักและ Replica ยังคง Synchronize กันอย่างสมบูรณ์

### **2. Asynchronous Replication Configuration**

ในการทำ Asynchronous Replication ฐานข้อมูลหลักจะส่งข้อมูลอัปเดตไปยัง Replica โดยไม่รอการยืนยัน

- ฐานข้อมูลหลักสามารถทำ Transaction ให้เสร็จได้ทันที ช่วยเพิ่มประสิทธิภาพและความเร็ว
- Replica อาจได้รับข้อมูลอัปเดตล่าช้าเล็กน้อย ซึ่งอาจทำให้ข้อมูลไม่สอดคล้องกันชั่วคราว

### **3. Semi-synchronous Replication Configuration**

Semi-synchronous Replication เป็นแนวทางแบบผสมที่รวมคุณสมบัติของ Synchronous และ Asynchronous Replication เข้าด้วยกัน

- ฐานข้อมูลหลักจะรอการยืนยันจาก Replica อย่างน้อยหนึ่งชุดก่อน Commit Transaction
- Replica ชุดอื่นจะได้รับข้อมูลอัปเดตแบบ Asynchronous ช่วยเพิ่มประสิทธิภาพในขณะที่ยังรักษาความสอดคล้องของข้อมูลให้อยู่ในระดับที่เหมาะสม

## **ความสำคัญ**

Database Replication มีความสำคัญด้วยเหตุผลหลายประการ:

- **High Availability:** Database Replication ช่วยให้ระบบมี [High Availability](https://www.geeksforgeeks.org/system-design/what-is-high-availability-in-system-design/) โดยทำให้ข้อมูลยังคงพร้อมใช้งานแม้เซิร์ฟเวอร์หนึ่งเครื่องจะล้มเหลว ทำให้แอปพลิเคชันทำงานต่อได้โดยไม่หยุดให้บริการ
- **Disaster Recovery:** Replication ช่วยรองรับ Disaster Recovery ด้วยการเก็บสำเนาสำรองไว้บนหลายเซิร์ฟเวอร์ ทำให้สามารถกู้คืนข้อมูลได้อย่างรวดเร็วหลังเกิดความล้มเหลว
- **Load Balancer / Load Balancing:** Replication ช่วยปรับปรุง Load Balancing โดยเปิดให้ [Load Balancer](https://www.geeksforgeeks.org/system-design/what-is-load-balancer-system-design/) ส่งคำขออ่านข้อมูลไปยังเซิร์ฟเวอร์ Replica ซึ่งช่วยลดภาระของฐานข้อมูลหลัก
- **Fault Tolerance:** Replication ช่วยให้ระบบมี [Fault Tolerance](https://www.geeksforgeeks.org/system-design/fault-tolerance-in-system-design/) โดยย้าย Traffic ไปยังเซิร์ฟเวอร์ Replica เครื่องอื่นเมื่อเซิร์ฟเวอร์เครื่องหนึ่งหยุดทำงาน
- **Scalability:** Replication ช่วยเพิ่ม [Scalability](https://www.geeksforgeeks.org/system-design/what-is-scalability/) ด้วยการกระจาย Traffic ของฐานข้อมูลไปยังหลายเซิร์ฟเวอร์ ทำให้รองรับผู้ใช้จำนวนมากขึ้นได้อย่างราบรื่น
- **Data Locality:** Replication ช่วยปรับปรุง Data Locality ด้วยการวาง Replica ไว้ใกล้กับผู้ใช้ เพื่อลด [Latency](https://www.geeksforgeeks.org/system-design/latency-in-system-design/) และเพิ่มประสิทธิภาพ

## **ความท้าทาย**

ความท้าทายบางประการของ Database Replication ได้แก่:

- **Data Consistency:** การรักษาความสอดคล้องของข้อมูลระหว่าง Replica อาจทำได้ยาก โดยเฉพาะในกรณีของ Asynchronous Replication ที่การทำ Replication ข้อมูลอาจเกิดความล่าช้า
- **Complexity:** Database Replication เพิ่มความซับซ้อนให้กับระบบ และต้องมีการตั้งค่าและดูแลอย่างรอบคอบ เพื่อให้การทำ Replication ข้อมูลถูกต้องและมีประสิทธิภาพ
- **Cost:** การติดตั้งและดูแลสภาพแวดล้อมฐานข้อมูลแบบ Replicated อาจมีค่าใช้จ่ายสูง โดยเฉพาะระบบขนาดใหญ่ที่มี Replica หลายชุด
- **Conflict Resolution:** ในระบบ Multi-Master Replication อาจเกิด Conflict เมื่อข้อมูลเดียวกันถูกแก้ไขพร้อมกันบน Replica หลายชุด จึงต้องใช้เทคนิคสำหรับจัดการ Conflict
- **Latency:** Synchronous Replication ซึ่งต้องรอการยืนยันจาก Replica ก่อน Commit Transaction อาจเพิ่ม Latency และส่งผลต่อประสิทธิภาพของฐานข้อมูลหลัก
