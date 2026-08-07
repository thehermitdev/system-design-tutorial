# **Low-Level Design หรือ LLD**

Low-Level Design (LLD) มีบทบาทสำคัญในการพัฒนาซอฟต์แวร์ โดยเปลี่ยนแนวคิดเชิงนามธรรมระดับสูงให้กลายเป็นองค์ประกอบที่มีรายละเอียดและสามารถนำไปพัฒนาได้จริง เพื่อให้นักพัฒนานำไปใช้สร้างระบบ

- LLD คือพิมพ์เขียวที่ช่วยให้นักพัฒนาทราบว่าจะนำองค์ประกอบเฉพาะของระบบไปพัฒนาอย่างไร เช่น คลาส เมธอด อัลกอริทึม และโครงสร้างข้อมูล
- ไม่ว่าเราจะทำงานกับสถาปัตยกรรมแบบ Microservice, Web Application หรือ Mobile App การเข้าใจ LLD เป็นสิ่งสำคัญสำหรับการสร้างระบบที่รองรับการขยายตัว ดูแลรักษาง่าย และมีประสิทธิภาพ

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260414102919491982/design.webp" />

## **ความแตกต่างระหว่าง HLD และ LLD**

ทั้ง HLD และ LLD มีความสำคัญในการออกแบบระบบ แต่เน้นรายละเอียดในระดับที่แตกต่างกัน โดย HLD ให้ภาพรวมของระบบในระดับกว้าง ส่วน LLD เน้นรายละเอียดในการนำไปพัฒนาจริง

1. **High-Level Design (HLD):** เน้นสถาปัตยกรรมโดยรวมของระบบ รวมถึง Framework, Database, การเชื่อมต่อระหว่าง Component และการทำงานของระบบในภาพรวม
2. **Low-Level Design (LLD):** เน้นการออกแบบ Component และ Module อย่างละเอียด รวมถึงการทำงานร่วมกัน, UML Diagram, พฤติกรรม ตลอดจน Algorithm และ Data Structure ที่ใช้

> **ตัวอย่าง:** ในระบบ E-commerce นั้น HLD จะกำหนด Component เช่น User Service, Payment Service และ Database ส่วน LLD จะกำหนดว่า Class “Order” ทำงานอย่างไร มี Method อะไรบ้าง และทำงานร่วมกับ Class อื่นอย่างไร

## **แนวคิดที่จำเป็นสำหรับการสร้าง LLD จาก HLD ที่กำหนด**

ในการเปลี่ยนจาก HLD ไปเป็น LLD โดยทั่วไปเราจะใช้ [Unified Modelling Language (UML) Diagram](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-introduction/) นอกจาก Diagram เหล่านี้แล้ว เรายังใช้หลักการ OOP, [SOLID Principles](https://www.geeksforgeeks.org/system-design/solid-principle-in-programming-understand-with-real-life-examples/) และ Design Pattern ในระหว่างการออกแบบอีกด้วย

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260414102919609290/roadmap_to_low_level_design_lld_-660.webp" />

### **ขั้นตอนที่ 1 ทำความเข้าใจหลักการ Object-Oriented**

Requirement ของผู้ใช้จะถูกนำมาแปลงเป็นแบบออกแบบด้วยแนวคิด OOP ซึ่งเป็นพื้นฐานของ Low-Level Design (LLD) การเข้าใจหลักการ OOP อย่างถ่องแท้ช่วยให้สามารถสร้าง Component ที่ดูแลรักษาง่าย รองรับการขยายตัว และมีโครงสร้างที่ดี

- **Encapsulation**: การรวมข้อมูลและ Method ที่ทำงานกับข้อมูลนั้นไว้ภายในหน่วยเดียวกัน
- **Inheritance**: กลไกที่ทำให้ Class ใหม่สามารถสืบทอด Property และ Method จาก Class ที่มีอยู่แล้วได้
- **Polymorphism**: ความสามารถของ Class ที่แตกต่างกันในการตอบสนองต่อ Method เดียวกันด้วยวิธีที่แตกต่างกัน
- **Abstraction**: การซ่อนรายละเอียดการทำงานที่ซับซ้อน และแสดงเฉพาะคุณสมบัติสำคัญของ Object

### **ขั้นตอนที่ 2 วิเคราะห์และออกแบบ Component**

LLD ต้องอาศัยการวิเคราะห์ปัญหาในโลกจริงและแยกปัญหาเหล่านั้นออกมาเป็นปัญหาในโลกของ Object ด้วยแนวคิด OOP ขั้นตอนนี้มีความสำคัญอย่างมาก เพราะเป็นการนำ Entity ในโลกจริงมาสร้างแบบจำลองเป็น Object และ Class

เราควรให้ความสำคัญกับ:

- การระบุ Class และ Object จาก Requirement ของระบบ
- การกำหนดความสัมพันธ์ระหว่าง Entity ต่างๆ เช่น Association และ Inheritance
- การใช้ SOLID Principles เพื่อให้การออกแบบสะอาด ดูแลรักษาง่าย และรองรับการขยายตัว

### **ขั้นตอนที่ 3 นำ Design Pattern มาใช้**

การพัฒนา Object-Oriented Design สามารถใช้ Design Pattern ช่วยสนับสนุนได้ โดย Design Pattern เป็นแนวทางที่นำกลับมาใช้ซ้ำได้สำหรับแก้ปัญหาที่พบบ่อย และช่วยสร้างระบบที่รองรับการขยายตัว ดูแลรักษาง่าย และมีประสิทธิภาพตามแนวทางปฏิบัติที่ได้รับการพิสูจน์แล้ว

- **Creational Patterns** (เช่น Singleton, Factory): Pattern เหล่านี้เกี่ยวข้องกับกลไกการสร้าง Object โดยพยายามสร้าง Object ด้วยวิธีที่เหมาะสมกับสถานการณ์
- **Behavioral Patterns** (เช่น Observer, Strategy): เน้นการสื่อสารระหว่าง Object และวิธีที่ Object ทำงานร่วมกัน
- **Structural Patterns** (เช่น Adapter, Composite): Pattern เหล่านี้เกี่ยวข้องกับการทำให้โครงสร้างของระบบและ Component เข้าใจและจัดการได้ง่ายขึ้น

### **ขั้นตอนที่ 4 การใช้ UML Diagram ใน LLD**

Unified Modeling Language (UML) ใช้สำหรับสร้างแบบจำลองและออกแบบระบบในรูปแบบภาพ เพื่อช่วยในการเปลี่ยนจาก HLD ไปเป็น LLD โดยแสดง Component และความสัมพันธ์ระหว่างกันอย่างชัดเจน ทำให้นักพัฒนาเข้าใจระบบได้ง่ายขึ้น

- **Class Diagrams**: แสดงโครงสร้างของระบบในรูปแบบของ Class และความสัมพันธ์ระหว่าง Class เหล่านั้น
- **Sequence Diagrams**: แสดงให้เห็นว่า Object ทำงานร่วมกันตามลำดับเวลาอย่างไร รวมถึงลำดับการเรียกใช้ Method
- **Activity Diagrams**: แสดง Workflow หรือกิจกรรมของ Component ในระบบ
- **State Diagrams**: แสดง State ต่างๆ ของ Component หรือ Object และการเปลี่ยนผ่านระหว่าง State เหล่านั้น
- **Use Case Diagrams**: กำหนด Functional Requirement ของระบบโดยแสดงรูปแบบการโต้ตอบต่างๆ ของผู้ใช้

Diagram เหล่านี้มีบทบาทสำคัญใน LLD เพราะช่วยแสดง Component และการทำงานร่วมกันในรูปแบบภาพอย่างชัดเจน

### **5. นำ SOLID Principles มาใช้**

SOLID คือชุดของหลักการ 5 ข้อที่นำมาใช้ตาม Requirement ของระบบหรือ Requirement สำหรับการออกแบบที่เหมาะสม เพื่อให้สามารถเขียน Code ที่รองรับการขยายตัว ยืดหยุ่น ดูแลรักษาง่าย และนำกลับมาใช้ซ้ำได้:

1. Single-responsibility principle (SRP)
2. Open-closed principle (OCP)
3. Liskov’s Substitution Principle(LSP)
4. Interface Segregation Principle (ISP)
5. Dependency Inversion Principle (DIP)

สิ่งสำคัญคือต้องเข้าใจว่า SOLID Principles เป็นเพียงแนวทาง ไม่ใช่กฎตายตัวที่ต้องปฏิบัติตามอย่างเคร่งครัด หัวใจสำคัญคือการหาสมดุลระหว่างการปฏิบัติตามหลักการเหล่านี้กับการพิจารณาความต้องการและข้อจำกัดเฉพาะของ Business Requirement

## **ประโยชน์**

Low-Level Design เป็นแนวทางที่ละเอียดและมีโครงสร้างสำหรับการสร้างระบบซอฟต์แวร์ ซึ่งมีประโยชน์หลายด้าน:

- **การทำงานของ Component ที่ชัดเจน**: LLD มีแผนอย่างละเอียดว่าแต่ละส่วนของซอฟต์แวร์จะทำงานอย่างไร ทำให้การพัฒนาและ Debug ง่ายขึ้น
- **Scalability และ Flexibility**: การออกแบบที่มีโครงสร้างที่ดีช่วยให้การแก้ไขหรือปรับปรุงส่วนต่างๆ ของระบบทำได้ง่ายขึ้นโดยไม่กระทบกับซอฟต์แวร์ทั้งระบบ
- **การสื่อสารที่ดีขึ้น**: LLD ช่วยให้สมาชิกในทีมสื่อสารกันได้อย่างมีประสิทธิภาพมากขึ้น เพราะทุกคนเข้าใจอย่างชัดเจนว่า Component ต่างๆ ทำงานอย่างไร
- **Code ที่สะอาดขึ้น**: การปฏิบัติตามหลักการออกแบบใน LLD ช่วยให้ Code สะอาดและเป็นระเบียบมากขึ้น รวมถึงลดโอกาสเกิดข้อผิดพลาด
- **เขียน Code ได้เร็วขึ้น**: LLD ที่เหมาะสมช่วยให้กระบวนการเขียน Code เร็วขึ้น เพราะนักพัฒนาสามารถทำตามแผนรายละเอียดที่ออกแบบไว้ก่อนหน้าได้

## **แนวทางปฏิบัติที่ดีสำหรับ Low-Level Design (LLD)**

แนวทางปฏิบัติที่ดีบางส่วนสำหรับการสร้าง Low-Level Design ที่ดี ได้แก่:

- **Modular Design:** พยายามแบ่งระบบออกเป็น Component ขนาดเล็กที่เป็นอิสระต่อกัน และแต่ละ Component มีหน้าที่เฉพาะ
- **Clear Interfaces:** กำหนด Interface ของแต่ละ Component ให้ชัดเจน ซึ่งควรรวมถึง Method, Input และ Output เพื่อช่วยให้การสื่อสารระหว่าง Component เป็นไปอย่างเหมาะสม
- **Use Design Patterns:** ใช้หลักการ OOPS เพื่อส่งเสริมการนำ Code กลับมาใช้ซ้ำ ความยืดหยุ่น และความสามารถในการดูแลรักษา
- **Adopt SOLID Principles:** ปฏิบัติตาม SOLID Principles ซึ่งจะช่วยให้การออกแบบมีความแข็งแรงและดูแลรักษาได้ง่ายขึ้น
- **Error Handling:** วางแผนล่วงหน้าสำหรับการจัดการ Error และการตรวจสอบความถูกต้องของระบบ โดยรวม Validation Check ไว้ในการออกแบบ

## **Roadmap สำหรับเรียนรู้ LLD**

หากต้องการเชี่ยวชาญ Low-Level Design ให้เรียนรู้ตามลำดับต่อไปนี้:

### **1. หลักการ Object-Oriented และหลักการออกแบบ**

- [**แนวคิด Object-Oriented Programming (OOPS)**](https://www.geeksforgeeks.org/system-design/object-oriented-programingoop-concepts-for-designing-sytems/)
- [**Object-Oriented Analysis and Design**](https://www.geeksforgeeks.org/software-engineering/object-oriented-analysis-and-design/)
- [**SOLID Principles**](https://www.geeksforgeeks.org/system-design/solid-principle-in-programming-understand-with-real-life-examples/)

### **2. Design Patterns**

- [**Creational Design Patterns**](https://www.geeksforgeeks.org/system-design/creational-design-pattern/)
- [**Behavioral Design Patterns**](https://www.geeksforgeeks.org/system-design/behavioral-design-patterns/)
- [**Structural Design Patterns**](https://www.geeksforgeeks.org/system-design/structural-design-patterns/)
- [**ควรเลือกใช้ Design Pattern แบบใดเมื่อไร?**](https://www.geeksforgeeks.org/system-design/design-patterns-cheat-sheet-when-to-use-which-design-pattern/)

### **3. UML และการสร้างแบบจำลองใน LLD**

- [**Class Diagrams**](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-class-diagrams/)
- [**Sequence Diagrams**](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-sequence-diagrams/)
- [**Activity Diagrams**](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-activity-diagrams/)
- [**State Diagrams**](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-state-diagrams/)
- [**Use Case Diagrams**](https://www.geeksforgeeks.org/system-design/use-case-diagram/)
- [**Object Diagrams**](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-object-diagrams/)

### **4. แนวทางปฏิบัติที่ดีสำหรับ LLD**

- [**Data Structures และ Algorithms สำหรับ System Design**](https://www.geeksforgeeks.org/system-design/data-structures-and-algorithms-for-system-design/)
- [**มาตรการด้าน Security ที่สำคัญใน System Design**](https://www.geeksforgeeks.org/system-design/essential-security-measures-in-system-design/)
- [**บทนำสู่ Modularity และ Interfaces**](https://www.geeksforgeeks.org/system-design/inroduction-to-modularity-and-interfaces-in-system-design/)
- [**ความแตกต่างระหว่าง LLD และ HLD**](https://www.geeksforgeeks.org/system-design/difference-between-high-level-design-and-low-level-design/)
- [**Performance เทียบกับ Scalability**](https://www.geeksforgeeks.org/system-design/performance-vs-scalability-in-system-design/)
- [**Speed เทียบกับ Quality**](https://www.geeksforgeeks.org/system-design/speed-vs-quality-in-system-design/)
- [**แนวทางปฏิบัติที่ดีสำหรับ Coding Standards**](https://www.geeksforgeeks.org/system-design/coding-standards-and-best-practices-for-system-design/)

### **5. กรณีศึกษาสำหรับ LLD**

- [**Low-Level Design ของระบบลิฟต์**](https://www.geeksforgeeks.org/system-design/elevator-system-low-level-design-lld/)
- [**Low-Level Design ของ Tic-Tac-Toe**](https://www.geeksforgeeks.org/system-design/low-level-design-of-tic-tac-toe-system-design/)
- [**Low-Level Design ของ Amazon**](https://www.geeksforgeeks.org/system-design/amazon-low-level-designlld/)
- [**Low-Level Design ของเครื่องขายสินค้าอัตโนมัติ**](https://www.geeksforgeeks.org/system-design/vending-machine-low-level-design/)

### **6. การเตรียมตัวสัมภาษณ์**

- [**เตรียมตัวสำหรับการสัมภาษณ์ Low-Level Design อย่างไร?**](https://www.geeksforgeeks.org/system-design/how-to-prepare-for-low-level-design-interviews/)
- [**คำถามสัมภาษณ์ Low-Level Design (LLD) ยอดนิยมปี 2024**](https://www.geeksforgeeks.org/system-design/top-low-level-system-designlld-interview-questions-2024/)
- [**หนังสือที่ดีที่สุดสำหรับเรียนรู้ Low-Level Design (LLD) ปี 2024**](https://www.geeksforgeeks.org/system-design/best-books-for-learning-low-level-designlld-2024/)
