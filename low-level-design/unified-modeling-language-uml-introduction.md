# **แผนภาพ Unified Modeling Language (UML)**

Unified Modeling Language (UML) คือภาษาสำหรับการสร้างแบบจำลองที่ใช้งานได้ทั่วไป เป้าหมายหลักของ UML คือการกำหนดวิธีมาตรฐานสำหรับแสดงภาพว่าระบบถูกออกแบบไว้อย่างไร ซึ่งค่อนข้างคล้ายกับแบบพิมพ์เขียวที่ใช้ในงานวิศวกรรมแขนงอื่น UML ไม่ใช่ภาษาโปรแกรม แต่เป็นภาษาที่ใช้การแสดงผลด้วยภาพ

- UML เป็นภาษาสำหรับการสร้างแบบจำลองที่เป็นมาตรฐาน (ได้รับการรับรองโดย ISO) ซึ่งช่วยให้ทีมมีแนวทางร่วมกันในการแสดงภาพและสื่อสารการออกแบบระบบ
- เราใช้แผนภาพ UML เพื่อแสดง****พฤติกรรมและโครงสร้างของระบบ
- UML ช่วยวิศวกรซอฟต์แวร์ นักธุรกิจ และสถาปนิกระบบในการสร้างแบบจำลอง การออกแบบ และการวิเคราะห์
- International Organization for Standardization (ISO) เผยแพร่ UML เป็นมาตรฐานที่ได้รับการรับรองในปี 2005 UML ได้รับการปรับปรุงตลอดหลายปีที่ผ่านมาและมีการทบทวนเป็นระยะ

> ***ตัวอย่าง:** ในระบบ E-commerce แผนภาพ UML สามารถแสดง Component เช่น User, Product และ Order รวมถึงวิธีที่ Component เหล่านี้โต้ตอบกันระหว่างกระบวนการ เช่น การสั่งซื้อสินค้า*
> 

## **ความจำเป็นของ UML**

UML มีความสำคัญต่อการแสดงภาพและสื่อสารการออกแบบระบบอย่างชัดเจนระหว่างผู้มีส่วนเกี่ยวข้องหลายฝ่ายในโครงการ

- Application ที่ซับซ้อนจำเป็นต้องอาศัยการทำงานร่วมกันและการวางแผนจากหลายทีม จึงต้องมีวิธีการสื่อสารที่ชัดเจนและกระชับ
- ผู้มีส่วนเกี่ยวข้องทางธุรกิจอาจไม่เข้าใจ Code ดังนั้น UML จึงช่วยอธิบาย Requirement, Functionality และ Process ของระบบด้วยภาพที่เข้าใจง่าย
- ช่วยประหยัดเวลาด้วยการให้ทีมสามารถมองเห็น Workflow, การโต้ตอบของ User และโครงสร้างระบบก่อนเริ่มพัฒนาจริง

## **ประเภทของแผนภาพ UML**

UML มีความเกี่ยวข้องกับการออกแบบและการวิเคราะห์เชิงวัตถุ UML ใช้ Element และสร้างความสัมพันธ์ระหว่าง Element เหล่านั้นเพื่อจัดทำเป็นแผนภาพ โดยสามารถแบ่งแผนภาพ UML ออกเป็นประเภทหลักๆ ได้ดังนี้:

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114108702973/uml_diagrams-660.webp" alt="UML Diagram" />

## **1. แผนภาพ UML เชิงโครงสร้าง**

[แผนภาพ UML เชิงโครงสร้าง](https://www.geeksforgeeks.org/system-design/structural-diagrams-unified-modeling-languageuml/) คือการแสดงภาพที่อธิบายส่วนที่เป็นโครงสร้างคงที่ของระบบ รวมถึง Class, Object, Component และความสัมพันธ์ระหว่างกัน ซึ่งช่วยให้เห็น Architecture ของระบบได้อย่างชัดเจน แผนภาพ UML เชิงโครงสร้างประกอบด้วยประเภทต่อไปนี้:

### **1. Class Diagram**

Class Diagram เป็นแผนภาพ UML ที่ถูกใช้งานอย่างแพร่หลายที่สุด และเป็นองค์ประกอบพื้นฐานของระบบซอฟต์แวร์เชิงวัตถุทั้งหมด เราใช้ Class Diagram เพื่อแสดงโครงสร้างคงที่ของระบบโดยแสดง Class, Method และ Attribute ของระบบ นอกจากนี้ Class Diagram ยังช่วยให้เราระบุความสัมพันธ์ระหว่าง Class หรือ Object ต่างๆ ได้

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114106919135/animal-660.webp" alt="Class Diagram" />

#### **Composite Structure Diagram**

เราใช้ Composite Structure Diagram เพื่อแสดงโครงสร้างภายในของ Class และจุดที่ Class นั้นโต้ตอบกับส่วนอื่นของระบบ

- Composite Structure Diagram แสดงความสัมพันธ์ระหว่างส่วนต่างๆ และการกำหนดค่าที่ส่งผลต่อพฤติกรรมของ Classifier (Class, Component หรือ Deployment Node)
- แผนภาพนี้แสดงโครงสร้างภายในของ Structured Classifier โดยใช้ Part, Port และ Connector
- มีลักษณะคล้าย Class Diagram แต่จะแสดงรายละเอียดของแต่ละส่วนมากกว่าการแสดง Class ทั้งหมดในภาพรวม

### **2. Object Diagram**

[Object Diagram](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-object-diagrams/) เปรียบได้กับภาพ Snapshot ของ Instance ต่างๆ ในระบบและความสัมพันธ์ที่มีอยู่ระหว่างกัน เนื่องจาก Object Diagram แสดงพฤติกรรมเมื่อ Object ถูกสร้างเป็น Instance แล้ว เราจึงสามารถศึกษาพฤติกรรมของระบบ ณ ช่วงเวลาหนึ่งได้

- Object Diagram มีลักษณะคล้าย Class Diagram แต่จะแสดง Instance ของ Class ต่างๆ ในระบบ
- เราใช้ Class Diagram เพื่อแสดง Classifier ที่มีอยู่จริงและความสัมพันธ์ระหว่างกัน
- ในทางกลับกัน Object Diagram จะแสดง Instance ที่เฉพาะเจาะจงของ Class และความสัมพันธ์ระหว่าง Instance เหล่านั้น ณ ช่วงเวลาหนึ่ง

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114108014883/link-660.webp" alt="Object Diagram" />

### **3. Component Diagram**

**Component Diagram** ใช้เพื่อแสดงว่า Physical Component ภายในระบบถูกจัดโครงสร้างไว้อย่างไร เราใช้แผนภาพนี้สำหรับสร้างแบบจำลองรายละเอียดของการ Implement

- Component Diagram แสดงความสัมพันธ์เชิงโครงสร้างระหว่าง Element ของระบบซอฟต์แวร์ และช่วยให้เราเข้าใจว่า Functional Requirement ถูกครอบคลุมโดยแผนการพัฒนาแล้วหรือไม่
- Component Diagram มีความสำคัญเมื่อเราออกแบบและสร้างระบบที่ซับซ้อน
- Component ต่างๆ ของระบบใช้ Interface เพื่อสื่อสารระหว่างกัน
- ในระบบสมัยใหม่ Component Diagram ถูกใช้อย่างแพร่หลายใน Microservices Architecture เพื่อแสดงขอบเขตของ Service, API และการสื่อสารระหว่าง Service ต่างๆ

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114107290456/component_based_diagram_example-660.webp" alt="Component Diagram" />

### **4. Deployment Diagram**

[Deployment Diagram](https://www.geeksforgeeks.org/system-design/deployment-diagram-unified-modeling-languageuml/) ใช้เพื่อแสดง Hardware และ Software ของระบบ โดยบอกให้เราทราบว่ามี Hardware Component ใดอยู่บ้าง และมี Software Component ใดทำงานอยู่บน Hardware เหล่านั้น

- เราแสดง System Architecture ในรูปแบบการกระจาย Software Artifact ไปยัง Target ต่างๆ ที่กระจายอยู่
- Artifact คือข้อมูลที่ถูกสร้างขึ้นโดย System Software
- แผนภาพนี้ถูกใช้เป็นหลักเมื่อ Software ถูกใช้งาน กระจาย หรือ Deploy ไปยังหลายเครื่องที่มี Configuration แตกต่างกัน

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114107469702/deployment_diagram_for_mobile_banking_android_services-660.webp" alt="Deployment Diagram" />

### **5. Package Diagram**

เราใช้ [Package Diagram](https://www.geeksforgeeks.org/system-design/package-diagram-introduction-elements-use-cases-and-benefits/) เพื่อแสดงว่า Package และ Element ภายในถูกจัดโครงสร้างไว้อย่างไร Package Diagram จะแสดง Dependency ระหว่าง Package ต่างๆ และองค์ประกอบภายในของแต่ละ Package

- Package ช่วยให้เราจัดกลุ่มแผนภาพ UML อย่างมีความหมายและทำให้แผนภาพเข้าใจได้ง่ายขึ้น
- แผนภาพนี้ถูกใช้เป็นหลักเพื่อจัดระเบียบ Class Diagram และ Use Case Diagram

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114108956520/web_shopping-660.webp" alt="Package Diagram" />

## **2. แผนภาพ UML เชิงพฤติกรรม**

[แผนภาพ UML เชิงพฤติกรรม](https://www.geeksforgeeks.org/system-design/behavior-diagrams-unified-modeling-languageuml/) คือการแสดงภาพที่อธิบายส่วนที่เป็น Dynamic ของระบบ โดยแสดงว่า Object โต้ตอบและมีพฤติกรรมอย่างไรเมื่อเวลาผ่านไปเพื่อตอบสนองต่อ Event ต่างๆ

### **1. State Machine Diagram**

[State Diagram](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-state-diagrams/) ใช้เพื่อแสดงสถานะของระบบหรือส่วนหนึ่งของระบบ ณ ช่วงเวลาที่กำหนด เป็น Behavioral Diagram ที่แสดงพฤติกรรมผ่านการเปลี่ยนสถานะแบบจำกัด

- State Diagram ยังเรียกว่า State Machine และ State-chart Diagram
- คำเหล่านี้มักถูกใช้แทนกัน ดังนั้นโดยสรุป State Diagram ใช้สำหรับสร้างแบบจำลองพฤติกรรมแบบ Dynamic ของ Class เพื่อตอบสนองต่อเวลาและสิ่งกระตุ้นภายนอกที่เปลี่ยนแปลงไป

*State Machine Diagram*

!card_swiped

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114107153329/card_swiped-660.webp" alt="State Machine Diagram" />

### **2. Activity Diagram**

เราใช้ [Activity Diagram](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-activity-diagrams/) เพื่อแสดง Flow of Control ภายในระบบ นอกจากนี้ยังสามารถใช้ Activity Diagram เพื่อแสดงขั้นตอนที่เกี่ยวข้องกับการทำงานของ Use Case ได้

- เราสร้างแบบจำลองกิจกรรมทั้งแบบ Sequential และ Concurrent ด้วย Activity Diagram ดังนั้นโดยพื้นฐานแล้ว เราใช้ Activity Diagram เพื่อแสดง Workflow ในรูปแบบภาพ
- Activity Diagram มุ่งเน้นเงื่อนไขของ Flow และลำดับที่ Flow นั้นเกิดขึ้น
- เราใช้ Activity Diagram เพื่ออธิบายหรือแสดงว่าอะไรเป็นสาเหตุให้ Event ใด Event หนึ่งเกิดขึ้น

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114107789034/input_the_number-660.webp" alt="Activity Diagram" />

### **3. Use Case Diagram**

[Use Case Diagram](https://www.geeksforgeeks.org/system-design/use-case-diagram/) ใช้เพื่อแสดง Functionality ของระบบหรือส่วนหนึ่งของระบบ และถูกใช้อย่างแพร่หลายเพื่อแสดง Functional Requirement ของระบบ รวมถึงการโต้ตอบกับ Agent ภายนอก (Actor)

- Use Case โดยพื้นฐานคือแผนภาพที่แสดง Scenario ต่างๆ ที่ระบบสามารถถูกใช้งานได้
- Use Case Diagram ช่วยให้เราเห็นภาพระดับสูงว่าระบบหรือส่วนหนึ่งของระบบทำอะไร โดยไม่ลงรายละเอียดเกี่ยวกับการ Implement

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114108210602/registered_customer-660.webp" />

### **4. Sequence Diagram**

[Sequence Diagram](https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-sequence-diagrams/) แสดงการโต้ตอบระหว่าง Object ตามลำดับ กล่าวคือ ลำดับที่การโต้ตอบเหล่านั้นเกิดขึ้น

- เราสามารถใช้คำว่า Event Diagram หรือ Event Scenario เพื่ออ้างถึง Sequence Diagram ได้เช่นกัน
- Sequence Diagram อธิบายว่า Object ในระบบทำงานอย่างไรและทำงานตามลำดับใด
- แผนภาพเหล่านี้ถูกใช้อย่างแพร่หลายโดยนักธุรกิจและนักพัฒนาซอฟต์แวร์ เพื่อจัดทำเอกสารและทำความเข้าใจ Requirement ของระบบทั้งใหม่และที่มีอยู่แล้ว

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114108830090/user-660.webp" />

### **5. Communication Diagram**

[Communication Diagram](https://www.geeksforgeeks.org/system-design/communication-diagram-unified-modeling-languageuml/) (เรียกว่า Collaboration Diagram ใน UML 1.x) ใช้เพื่อแสดง Message ที่ถูกแลกเปลี่ยนระหว่าง Object ตามลำดับ

- Communication Diagram มุ่งเน้น Object และความสัมพันธ์ระหว่าง Object เป็นหลัก
- เราสามารถแสดงข้อมูลที่คล้ายกันด้วย Sequence Diagram ได้ แต่ Communication Diagram จะแสดง Object และ Link ในรูปแบบที่อิสระกว่า

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114107616545/event_request_window-660.webp" alt="Communication Diagram" />

### **6. Interaction Overview Diagram**

[Interaction Overview Diagram (IOD)](https://www.geeksforgeeks.org/system-design/interaction-overview-diagrams-unified-modeling-language-uml/) เป็นแผนภาพ UML (Unified Modeling Language) ประเภทหนึ่งที่แสดง Flow ของการโต้ตอบระหว่าง Element ต่างๆ ภายในระบบหรือ Process โดยให้ภาพรวมระดับสูงว่าการโต้ตอบเกิดขึ้นอย่างไร รวมถึงลำดับของ Action, Decision และการโต้ตอบระหว่าง Component หรือ Object ต่างๆ

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260331114108492733/sd_online_shopping-660.webp" alt="Interaction Overview Diagram" />

#### **สิ่งที่เพิ่มเข้ามาใน UML 2.0**

- มีการนำแนวทางพัฒนาซอฟต์แวร์ เช่น Agile เข้ามารวมไว้ และขยายขอบเขตของข้อกำหนด UML เดิมให้กว้างขึ้น
- เดิม UML กำหนดแผนภาพไว้ 9 ประเภท UML 2.x เพิ่มจำนวนแผนภาพจาก 9 เป็น 13 ประเภท โดยแผนภาพ 4 ประเภทที่ถูกเพิ่มเข้ามาคือ Timing Diagram, Communication Diagram, Interaction Overview Diagram และ Composite Structure Diagram นอกจากนี้ UML 2.x ยังเปลี่ยนชื่อ Statechart Diagram เป็น State Machine Diagram
- UML 2.x เพิ่มความสามารถในการแบ่งระบบซอฟต์แวร์ออกเป็น Component และ Sub-component

## **เครื่องมือสำหรับสร้างแผนภาพ UML**

มีเครื่องมือหลายประเภทสำหรับสร้างแผนภาพ Unified Modeling Language (UML) ซึ่งถูกใช้งานทั่วไปในการพัฒนาซอฟต์แวร์เพื่อแสดง System Architecture, Design และ Implementation ในรูปแบบภาพ ต่อไปนี้คือเครื่องมือยอดนิยมสำหรับสร้างแผนภาพ UML:

- **Lucidchart:** Lucidchart เป็นเครื่องมือสร้างแผนภาพบนเว็บที่รองรับแผนภาพ UML ใช้งานง่ายและรองรับการทำงานร่วมกัน โดยเปิดให้ผู้ใช้หลายคนทำงานบนแผนภาพร่วมกันแบบ Real-time
- **Draw.io:** Draw.io เป็นเครื่องมือสร้างแผนภาพบนเว็บที่ใช้งานได้ฟรีและรองรับแผนภาพหลายประเภท รวมถึง UML สามารถเชื่อมต่อกับบริการ Cloud Storage หลายประเภทและใช้งานแบบ Offline ได้
- **Visual Paradigm:** Visual Paradigm มีชุดเครื่องมือที่ครอบคลุมสำหรับการพัฒนาซอฟต์แวร์ รวมถึงการสร้างแผนภาพ UML มีทั้งเวอร์ชัน Online และ Desktop และรองรับแผนภาพ UML หลากหลายประเภท
- **StarUML:** StarUML เป็นเครื่องมือสร้างแบบจำลอง UML แบบ Open-source ที่มี Interface ใช้งานง่าย รองรับแผนภาพมาตรฐาน UML 2.x และเปิดให้ผู้ใช้ปรับแต่งและขยาย Functionality ผ่าน Plugin ได้
