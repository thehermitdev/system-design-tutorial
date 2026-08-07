# **Web Server และ Application Server ในการออกแบบระบบ**

Web Server และ Application Server เป็นองค์ประกอบสำคัญในการออกแบบระบบที่ทำหน้าที่จัดการคำขอจากผู้ใช้และส่งผลลัพธ์กลับอย่างมีประสิทธิภาพ โดย Web Server จะจัดการการสื่อสารกับ Client ส่วน Application Server จะประมวลผล Business Logic และการทำงานแบบ Dynamic

- Web Server จัดการคำขอ HTTP ให้บริการ Static Content และจัดการการสื่อสารระหว่าง Client กับ Server
- Application Server ทำงานกับ Business Logic ประมวลผลข้อมูลแบบ Dynamic และสร้าง Response สำหรับคำขอจาก Client

## **Web Server**

Web Server คือระบบที่จัดเก็บ ประมวลผล และส่งมอบเนื้อหาบนเว็บให้กับผู้ใช้ผ่านอินเทอร์เน็ต โดยจะรับคำขอจาก Client (เช่น Browser) และตอบกลับด้วยหน้าเว็บ รูปภาพ หรือข้อมูล Web Server สามารถหมายถึงได้ทั้ง Hardware (เครื่อง) และ Software ที่ใช้จัดการคำขอเหล่านี้

- ใช้ Hosting เว็บไซต์และให้บริการเนื้อหาแก่ผู้ใช้ โดยทำงานด้วย Web Server Software เช่น Apache หรือ IIS
- ต้องเชื่อมต่ออินเทอร์เน็ตอย่างต่อเนื่องเพื่อรองรับคำขอที่เข้ามาจาก Client

> **ตัวอย่าง:** เมื่อคุณพิมพ์ URL ของเว็บไซต์ใน Browser คำขอจะถูกส่งไปยัง Web Server ซึ่งจะประมวลผลและส่งหน้าเว็บกลับมาเพื่อแสดงผล

Web Server ทุกเครื่องที่เชื่อมต่อกับอินเทอร์เน็ตจะได้รับ Address ที่ไม่ซ้ำกัน ซึ่งประกอบด้วยตัวเลข 4 ชุดที่คั่นด้วยจุด เช่น **68.122.31.125**

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260411151404076805/web_broser_request_to_web_server-660.webp" alt="Web Server" />

### **ประเภทของ Web Server**

Web Server สามารถแบ่งประเภทตามรูปแบบการ Hosting เว็บไซต์และวิธีจัดการ Traffic

- **Shared Hosting:** Hosting หลายเว็บไซต์ (มักมี 100 เว็บไซต์ขึ้นไป) บน Server เครื่องเดียว มีต้นทุนคุ้มค่าและเหมาะกับเว็บไซต์ขนาดเล็กหรือเว็บไซต์ส่วนตัว
- **Dedicated Hosting:** Server หนึ่งเครื่องถูกจัดสรรให้กับเว็บไซต์หนึ่งหรือไม่กี่เว็บไซต์ ทำให้มีประสิทธิภาพ การควบคุม และความปลอดภัยที่ดีกว่า
- **Custom Hosting:** สร้างขึ้นโดยเฉพาะสำหรับแอปพลิเคชันขนาดใหญ่ที่มีความต้องการเฉพาะ สามารถปรับแต่งได้เต็มรูปแบบและรองรับการขยายระบบได้สูง

เว็บไซต์ขนาดเล็กหรือเว็บไซต์ส่วนตัวมักใช้ Shared Hosting ส่วนแอปพลิเคชันที่มี Traffic สูงจะนิยมใช้ Dedicated Hosting หรือ Custom Hosting เพื่อให้ได้ประสิทธิภาพและการควบคุมที่ดีกว่า

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260411151403846243/shared_and_dedicated_hosts-660.webp" alt="Shared and Dedicated Hosts" />

### **การทำงาน**

Web Server จะประมวลผลคำขอจาก Client และส่ง Web Content ที่ต้องการกลับไปโดยใช้ Protocol HTTP/HTTPS โดยทำหน้าที่เป็นตัวกลางระหว่างผู้ใช้ (Browser) กับระบบ Backend

- เมื่อผู้ใช้ส่งคำขอ (เช่น เปิดเว็บไซต์) Browser จะส่ง HTTP Request ไปยัง Web Server
- หากเนื้อหาที่ร้องขอเป็น Static Content (HTML, CSS, รูปภาพ) Web Server จะส่งเนื้อหานั้นกลับไปยัง Client โดยตรง
- หากคำขอเป็น Dynamic Content Web Server จะส่งต่อไปยัง Application Server หรือ Backend Service เพื่อประมวลผล
- Application Server จะประมวลผลคำขอ (เช่น ดึงข้อมูลจาก Database) และส่งผลลัพธ์กลับไปยัง Web Server
- สุดท้าย Web Server จะส่ง Response กลับไปยัง Browser ของ Client

> **ตัวอย่าง:** เมื่อคุณเปิดเว็บไซต์ Shopping หน้า Homepage (Static Content) จะโหลดจาก Web Server โดยตรง แต่เมื่อคุณค้นหาสินค้า คำขอจะถูกส่งไปยัง Backend ซึ่งจะดึงผลลัพธ์จาก Database และส่งกลับผ่าน Web Server ไปยัง Browser ของคุณ

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260411151404139226/working_of_server-660.webp" alt="Working of server" />

### **บทบาทของ Web Server**

Web Server มีบทบาทสำคัญในการจัดการคำขอจาก Client และส่งมอบ Web Content อย่างมีประสิทธิภาพและปลอดภัย

- **การจัดการคำขอจาก Client:** Web Server รับและประมวลผลคำขอ HTTP/HTTPS ที่เข้ามาจาก Client (Browser) และส่งต่อไปยัง Resource หรือ Service ที่เหมาะสม
- **การให้บริการ Static และ Dynamic Content:** ให้บริการ Static Content (HTML, CSS, รูปภาพ) โดยตรง และทำงานร่วมกับ Application Server เพื่อสร้างและส่งมอบ Dynamic Content
- **Load Balancing:** ในระบบขนาดใหญ่ Web Server จะกระจาย Traffic ที่เข้ามาไปยัง Backend Server หลายเครื่อง เพื่อเพิ่มประสิทธิภาพและป้องกันการทำงานหนักเกินไป
- **Content Delivery & Caching:** Web Server ทำ Cache เนื้อหาที่ถูกเรียกใช้งานบ่อย เพื่อลด Response Time และลดภาระของ Server
- **SSL/TLS Termination:** จัดการการเข้ารหัสและถอดรหัสข้อมูล เพื่อให้การสื่อสารระหว่าง Client กับ Server มีความปลอดภัยโดยไม่เพิ่มภาระให้ระบบ Backend

### **Static Web Server Vs Dynamic Web Server**

Web Server สามารถให้บริการได้ทั้ง Static Content และ Dynamic Content ตามประเภทของแอปพลิเคชันและการประมวลผลใน Backend

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260411151403948173/static_website-660.webp" alt="Static and Dynamic Website" />

**Static Web Server**: ให้บริการเนื้อหาตามที่จัดเก็บไว้โดยไม่มีการแก้ไข

- ส่งไฟล์ เช่น HTML, CSS และรูปภาพ ไปยัง Browser โดยตรง
- ทำงานได้เร็วกว่าเพราะไม่ต้องมีการประมวลผลเพิ่มเติม
- เหมาะสำหรับ Blog, Portfolio และเว็บไซต์แบบเรียบง่าย

**Dynamic Web Server**: สร้างและอัปเดตเนื้อหาแบบ Real-time โดยใช้ Software เพิ่มเติม เช่น Application Server และ Database

- ประมวลผลข้อมูลจากผู้ใช้และดึงข้อมูลแบบ Dynamic
- ให้เนื้อหาที่ปรับให้เหมาะกับผู้ใช้และสามารถโต้ตอบได้
- เหมาะสำหรับ Social Media, E-commerce และ Web App

### **Protocol ที่ใช้**

Web Server ใช้ Communication Protocol มาตรฐานในการแลกเปลี่ยนข้อมูลกับ Client ผ่านอินเทอร์เน็ต

- **HTTP (HyperText Transfer Protocol):** ใช้สำหรับส่งหน้าเว็บและ Resource ระหว่าง Client กับ Server
- **HTTPS:** HTTP เวอร์ชันที่ปลอดภัย โดยใช้การเข้ารหัส SSL/TLS เพื่อปกป้องข้อมูลระหว่างการรับส่ง
- **FTP (File Transfer Protocol):** ใช้สำหรับถ่ายโอนไฟล์ระหว่างระบบ มักใช้ในการอัปโหลดเนื้อหาเว็บไซต์

### **ตัวอย่าง**

Web Server ที่ได้รับความนิยมและถูกใช้งานจริง ได้แก่:

- **Apache HTTP Server:** หนึ่งใน Web Server ที่ได้รับความนิยมมากที่สุด ใช้จัดการ HTTP Request และให้บริการหน้าเว็บและไฟล์ได้อย่างมีประสิทธิภาพ มีความน่าเชื่อถือสูงและมี Ecosystem ขนาดใหญ่รองรับ
- **Tomcat Server:** นิยมใช้กับ Web Application ที่พัฒนาด้วย Java ทำหน้าที่ได้ทั้งเป็น Web Server และ Servlet Container แต่ไม่ใช่ Application Server แบบเต็มรูปแบบ
- **Node.js Server:** มี HTTP Module ในตัวที่ช่วยให้นักพัฒนาสามารถสร้าง Web Server ที่มีน้ำหนักเบาและทำงานได้รวดเร็ว โดยเฉพาะสำหรับแอปพลิเคชันแบบ Real-time

## **Application Server**

Application Server ถูกออกแบบมาเพื่อทำงานและจัดการ Business Logic รวมถึงการทำงานที่ซับซ้อนซึ่งแอปพลิเคชันต้องการ โดยจัดเตรียม Environment (Hardware + Software) สำหรับทำงานแบบ Dynamic และประมวลผลคำขอจาก Client ที่มากกว่าการส่งมอบเนื้อหาแบบง่ายๆ

- จัดการ Logic และการคำนวณที่ซับซ้อน (เช่น การประมวลผลคำขอและ Transaction) และทำงานร่วมกับ Database/Service เพื่อสร้าง Dynamic Content
- จัดเตรียม Environment สำหรับรันแอปพลิเคชัน เช่น ระบบ Enterprise หรือระบบที่ทำงานบน Cloud

> **ตัวอย่าง:** เมื่อคุณ Login เข้าแอปธนาคาร Application Server จะตรวจสอบข้อมูล Credentials ของคุณ ดึงข้อมูลบัญชีจาก Database และส่งผลลัพธ์กลับไปยัง Web Server เพื่อแสดงผลใน Browser

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260411152025366950/application_server-660.webp" alt="Application Server" />

> **หมายเหตุ:** Application Server ถูกใช้เมื่อระบบต้องการการประมวลผลหนักหรือการทำงานแบบ Dynamic ซึ่ง Web Server เพียงอย่างเดียวไม่สามารถจัดการได้อย่างมีประสิทธิภาพ

### **การทำงาน**

Application Server ทำงานตาม Client-Server Model โดยประมวลผลคำขอจากผู้ใช้ ทำงานกับ Business Logic และส่ง Dynamic Response กลับไป โดยทำหน้าที่เป็น Layer หลักที่จัดการ Functionality ของแอปพลิเคชันและการประมวลผลข้อมูล

- Client (Browser/Mobile App) ส่งคำขอไปยัง Web Server
- Web Server ส่งต่อ Dynamic Request ไปยัง Application Server
- Application Server ทำงานกับ Business Logic (เช่น Authentication, Transaction)
- Application Server ติดต่อกับ Database หรือ External Service เพื่อดึงหรืออัปเดตข้อมูล
- ผลลัพธ์ที่ประมวลผลแล้วจะถูกส่งกลับไปยัง Web Server ซึ่งจะส่งต่อกลับไปยัง Client

**Layer ที่เกี่ยวข้อง:**

- Presentation Layer: จัดการ User Interface และรูปแบบ Request/Response
- Application Layer: ประกอบด้วย Business Logic และการประมวลผล
- Data Access Layer: จัดการการติดต่อกับ Database

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260411151403763567/clien-660.webp" alt="clien" />

### **Application Server ที่ได้รับความนิยม**

Application Server จัดเตรียม Environment สำหรับรันและจัดการแอปพลิเคชัน โดยรองรับ Technology และ Framework ที่แตกต่างกัน

- **Apache Tomcat:** นิยมใช้อย่างแพร่หลายสำหรับ Web Application ที่พัฒนาด้วย Java ทำหน้าที่เป็น Servlet Container และ Application Server แบบ Lightweight
- **JBoss (WildFly):** Application Server แบบ Java EE ที่มีความสามารถครบถ้วน ใช้สำหรับ Enterprise Application
- **IBM WebSphere Application Server:** Server ระดับ Enterprise ที่ออกแบบมาสำหรับแอปพลิเคชันขนาดใหญ่ มีความปลอดภัยและประสิทธิภาพสูง
- **Oracle WebLogic Server:** Application Server ที่มีความแข็งแกร่ง ใช้สำหรับระบบ Enterprise ที่มีความสำคัญสูง
- **Microsoft IIS (Internet Information Services):** รองรับแอปพลิเคชัน ASP.NET และนิยมใช้ใน Environment ที่ใช้ Windows

### **ข้อดี**

Application Server มีความสามารถที่ทรงพลังสำหรับจัดการแอปพลิเคชันที่ซับซ้อนและเป็น Dynamic

- **จัดการ Logic ที่ซับซ้อน:** ประมวลผล Business Logic และการคำนวณหนักได้อย่างมีประสิทธิภาพ
- **Scalability:** สามารถรองรับจำนวนผู้ใช้และ Traffic ที่เพิ่มขึ้นได้เมื่อมีการกำหนดค่าอย่างเหมาะสม
- **รองรับการ Integration:** สามารถเชื่อมต่อกับ Database, API และ External Service ได้ง่าย
- **ความสามารถด้าน Security:** รองรับ Authentication, Authorization และ Transaction ที่ปลอดภัย

### **ข้อเสีย**

แม้ Application Server จะมีข้อดี แต่ก็มีข้อจำกัดบางประการ

- **มีความซับซ้อนสูง:** ตั้งค่าและจัดการได้ซับซ้อนกว่า Web Server
- **มีต้นทุนสูงกว่า:** การบำรุงรักษาและ Deploy อาจมีค่าใช้จ่ายสูง
- **Latency Overhead:** การประมวลผลเพิ่มเติมอาจทำให้ Response Time เพิ่มขึ้น
- **ไม่จำเป็นสำหรับแอปที่เรียบง่าย:** ซับซ้อนเกินความจำเป็นสำหรับเว็บไซต์ขนาดเล็กหรือ Static Website

## **Web Server Vs Application Server**

Server ทั้งสองประเภทมีความแตกต่างกันตามบทบาท โดย Web Server ทำหน้าที่จัดการคำขอจาก Client และส่งมอบเนื้อหา ส่วน Application Server ทำหน้าที่ประมวลผล Business Logic และการทำงานแบบ Dynamic

| **Web Server** | **Application Server** |
| --- | --- |
| จัดการคำขอ HTTP/HTTPS | จัดการ Business Logic และการประมวลผล |
| ให้บริการ Static Content | สร้าง Dynamic Content |
| Lightweight และทำงานได้เร็วกว่า | ใช้ Resource มากกว่าและมีขนาดใหญ่กว่า |
| มีการติดต่อกับ Database อย่างจำกัดหรือไม่มีเลย | ติดต่อกับ Database โดยตรง |
| **ตัวอย่าง:** Apache, Nginx | **ตัวอย่าง:** Tomcat, WebLogic |
