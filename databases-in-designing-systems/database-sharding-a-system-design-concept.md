# **Database Sharding - การออกแบบระบบ**

Database Sharding เป็นเทคนิคที่ใช้ขยายขนาดฐานข้อมูลด้วยการกระจายข้อมูลไปยังเซิร์ฟเวอร์หลายเครื่อง ช่วยเพิ่มประสิทธิภาพและรองรับชุดข้อมูลขนาดใหญ่ได้อย่างมีประสิทธิภาพ

- ข้อมูลจะถูกแบ่งออกเป็นส่วนย่อยที่เรียกว่า Shard โดยแต่ละ Shard จะถูกจัดเก็บไว้ใน Database Instance ที่แตกต่างกันเพื่อกระจายภาระงาน
- ช่วยลดภาระของฐานข้อมูลเพียงเครื่องเดียว ทำให้ประสิทธิภาพของ Query และความสามารถในการขยายระบบดีขึ้น

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20250930141857544212/database.webp" alt="database" />

โดยพื้นฐานแล้ว นี่คือรูปแบบสถาปัตยกรรมฐานข้อมูลที่เราแบ่งชุดข้อมูลขนาดใหญ่ออกเป็นส่วนย่อยๆ (Logical Shard) แล้วจัดเก็บหรือกระจายส่วนเหล่านี้ไปยังเครื่องหรือโหนดฐานข้อมูลที่แตกต่างกัน (Physical Shard)

- แต่ละส่วนหรือ Partition จะเรียกว่า "Shard" และแต่ละ Shard จะมี Database Schema เหมือนกับฐานข้อมูลต้นฉบับ
- เรากระจายข้อมูลในลักษณะที่แต่ละ Row จะอยู่ใน Shard เพียงหนึ่งเดียวเท่านั้น
- เป็นกลไกที่ดีในการเพิ่มความสามารถในการขยายระบบของแอปพลิเคชัน

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260114163512510798/database_sharding-660.webp" alt="database_sharding" />

## **วิธีการทำ Sharding**

Sharding สามารถทำได้ด้วยการแบ่งข้อมูลแบบ Range-based, Hash-based, Directory-based หรือ Geographic-based เพื่อกระจายข้อมูลไปยังเซิร์ฟเวอร์หลายเครื่อง

### **1. Key Based Sharding**

Key Based Sharding เป็นเทคนิคที่รู้จักกันในชื่อ Hash-based Sharding โดยเราจะนำค่าของ Entity เช่น Customer ID, อีเมลของลูกค้า, IP Address ของ Client, รหัสไปรษณีย์ เป็นต้น มาใช้เป็น Input ของ Hash Function กระบวนการนี้จะสร้าง Hash Value ซึ่งใช้กำหนดว่าเราต้องใช้ Shard ใดในการจัดเก็บข้อมูล

- เราต้องคำนึงว่าค่าที่ส่งเข้า Hash Function ควรมาจาก **Column เดียวกัน** (Shard Key) เพื่อให้แน่ใจว่าข้อมูลถูกจัดวางอย่างถูกต้องและสม่ำเสมอ
- โดยพื้นฐานแล้ว Shard Key ทำหน้าที่คล้าย Primary Key หรือ Unique Identifier สำหรับแต่ละ Row

> ***ตัวอย่าง**: คุณมี Database Server 3 เครื่อง และแต่ละ Request มี Application ID ซึ่งจะเพิ่มขึ้นทีละ 1 ทุกครั้งที่มีการลงทะเบียน Application ใหม่*

เพื่อกำหนดว่าควรจัดเก็บข้อมูลไว้ที่ Server ใด เราจะนำ Application ID เหล่านี้ไปทำ Modulo ด้วยเลข 3 จากนั้นใช้เศษที่ได้เพื่อระบุ Server ที่จะจัดเก็บข้อมูล

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260114163512087066/key_based_sharding-660.webp" alt="key_based_sharding" />

#### **ข้อดี**

Key-based Sharding ช่วยกระจายข้อมูลไปยัง Shard ต่างๆ โดยใช้กลไก Hashing

- **การกำหนด Key:** กำหนดแต่ละ Key ให้กับ Shard ที่เฉพาะเจาะจง เพื่อให้การกระจายข้อมูลมีความสม่ำเสมอและคงที่
- **การเพิ่มประสิทธิภาพ Range Query:** สามารถปรับแต่งให้รองรับ Query ที่ทำงานกับช่วงของ Key ที่ต่อเนื่องกันได้อย่างมีประสิทธิภาพ

#### **ข้อเสีย**

แม้จะมีประสิทธิภาพ แต่การเลือก Shard Key ที่ไม่เหมาะสมอาจก่อให้เกิดปัญหาด้านประสิทธิภาพได้

- **การกระจายข้อมูลไม่สม่ำเสมอ:** อาจเกิดขึ้นได้หาก Sharding Key ไม่ได้กระจายตัวอย่างเหมาะสม
- **ข้อจำกัดด้าน Scalability:** ความสามารถในการขยายระบบอาจถูกจำกัดเมื่อ Key บางค่ามี Traffic สูง หรือข้อมูลมีการกระจายแบบไม่สมดุล

### **2. Horizontal หรือ Range Based Sharding**

ใน Horizontal หรือ Range Based Sharding เราจะแบ่งข้อมูลออกเป็นส่วนต่างๆ ตามช่วงของค่าที่ระบุในแต่ละ Record สมมติว่าคุณมีฐานข้อมูลที่เก็บชื่อและอีเมลของลูกค้าออนไลน์ คุณสามารถแบ่งข้อมูลนี้ออกเป็นสอง Shard ได้

- ใน Shard หนึ่ง คุณสามารถเก็บข้อมูลของลูกค้าที่ชื่อขึ้นต้นด้วย A-P
- ในอีก Shard หนึ่ง ให้เก็บข้อมูลของลูกค้าที่เหลือ

> **ตัวอย่าง**: ในฐานข้อมูลลูกค้า Shard หนึ่งอาจเก็บ Record ที่ชื่อขึ้นต้นด้วย A–P ขณะที่อีก Shard เก็บ Record ที่ชื่อขึ้นต้นด้วย Q–Z

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260114163512296190/horizontal_or_range_based_sharding-660.webp" alt="horizontal_or_range_based_sharding" />

#### **ข้อดี**

Horizontal หรือ Range-based Sharding กระจายข้อมูลไปยังหลาย Shard โดยอิงตามช่วงของค่าที่กำหนด

- **Scalability:** Horizontal หรือ Range-based Sharding ช่วยให้ขยายระบบได้อย่างราบรื่นด้วยการกระจายข้อมูลไปยังหลาย Shard เพื่อรองรับชุดข้อมูลที่เพิ่มขึ้น
- **ประสิทธิภาพที่ดีขึ้น:** การกระจายข้อมูลระหว่าง Shard ช่วยเพิ่มประสิทธิภาพของ Query ด้วยการประมวลผลแบบขนาน ทำให้แต่ละ Shard จัดการข้อมูลเพียงส่วนย่อยที่มีขนาดเล็กลงและทำงานได้เร็วขึ้น

#### **ข้อเสีย**

การจัดการและ Query ข้อมูลข้ามหลาย Shard อาจเพิ่มความซับซ้อน

- **ความซับซ้อนของ Query ข้าม Shard:** การประสานงาน Query ที่เกี่ยวข้องกับหลาย Shard อาจทำได้ยาก
- **การกระจายข้อมูลไม่สม่ำเสมอ:** หากจัดการการกระจายข้อมูลไม่ดี อาจทำให้แต่ละ Shard มีภาระงานไม่เท่ากัน

### **3. Vertical Sharding**

Vertical Sharding แบ่งฐานข้อมูลด้วยการแยก Column ของ Table ไปไว้ใน Shard หรือ Table ที่แตกต่างกัน แต่ละ Shard จะเก็บชุด Column ที่เกี่ยวข้องกับ Feature หรือ Functionality เฉพาะ วิธีนี้ช่วยกระจายภาระงานและจัดการ Table ขนาดใหญ่ได้อย่างมีประสิทธิภาพมากขึ้น

- แต่ละ Shard จะมี Column เพียงบางส่วน ขณะที่ Row ยังคงมีความสัมพันธ์เชิงตรรกะกับ Entity เดียวกัน
- Feature ที่แตกต่างกันของ Entity สามารถจัดเก็บไว้บนเครื่องแยกกันเพื่อเพิ่มประสิทธิภาพและความสะดวกในการจัดการ

> ***ตัวอย่าง**: บน Twitter ผู้ใช้อาจมี Profile, จำนวนผู้ติดตาม และ Tweet ที่โพสต์ด้วยตนเอง เราสามารถวาง Profile ของผู้ใช้ไว้ใน Shard หนึ่ง ผู้ติดตามไว้ใน Shard ที่สอง และ Tweet ไว้ใน Shard ที่สาม*

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260114163511692882/vertical_sharding-660.webp" alt="vertical_sharding" />

#### **ข้อดี**

Vertical Sharding แบ่งฐานข้อมูลโดยแยก Column ไปยัง Shard ต่างๆ ตาม Functionality

- **ประสิทธิภาพของ Query:** Vertical Sharding สามารถเพิ่มประสิทธิภาพของ Query ได้โดยให้แต่ละ Shard มุ่งจัดการ Column เฉพาะกลุ่ม การแยกหน้าที่นี้ช่วยให้ Query ที่ใช้เพียงบาง Column ทำงานได้อย่างมีประสิทธิภาพมากขึ้น
- **Query ที่ง่ายขึ้น:** Query ที่ต้องใช้ Column เฉพาะชุดสามารถทำให้ง่ายขึ้นได้ เพราะต้องติดต่อเฉพาะ Shard ที่มี Column ที่เกี่ยวข้องเท่านั้น

#### **ข้อเสีย**

การแยก Column ไปยังหลาย Shard อาจทำให้เกิดความท้าทายด้านการดำเนินงานและภาระงาน

- **ความเสี่ยงในการเกิด Hotspot:** Shard บางตัวอาจกลายเป็น Hotspot หากมี Column ที่ถูกเข้าถึงบ่อย ส่งผลให้ภาระงานกระจายไม่สมดุล
- **ความท้าทายในการเปลี่ยน Schema:** การเปลี่ยน Schema เช่น การเพิ่มหรือลบ Column อาจทำได้ยากขึ้นในระบบที่ใช้ Vertical Sharding การเปลี่ยนแปลงอาจกระทบหลาย Shard และต้องมีการประสานงานอย่างรอบคอบ

### **4. Directory-Based Sharding**

ใน Directory-Based Sharding เราจะสร้างและดูแล Lookup Service หรือ Lookup Table สำหรับฐานข้อมูลต้นฉบับ โดยพื้นฐานแล้ว เราใช้ Shard Key สำหรับ Lookup Table และทำ Mapping ให้กับแต่ละ Entity ที่อยู่ในฐานข้อมูล วิธีนี้ช่วยให้เราติดตามได้ว่า Database Shard ใดเก็บข้อมูลใดอยู่

> ***ตัวอย่าง**: ฐานข้อมูลผู้ใช้อาจใช้ Lookup Table ที่จับคู่ User ID แต่ละตัวกับ Shard ที่จัดเก็บข้อมูลของผู้ใช้นั้น เมื่อมี Request เข้ามา ระบบจะตรวจสอบ Lookup Table ก่อน จากนั้นจึงส่ง Query ไปยัง Shard ที่ถูกต้อง*

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260114163511883644/pre_sharded_table-660.webp" alt="pre_sharded_table" />

Lookup Table จะเก็บชุดข้อมูลแบบคงที่เกี่ยวกับตำแหน่งที่สามารถค้นหาข้อมูลเฉพาะได้

จากภาพด้านบน คุณจะเห็นว่าเราใช้ Delivery Zone เป็น Shard Key:

- ขั้นแรก Client Application จะ Query ไปยัง Lookup Service เพื่อค้นหา Shard (Database Partition) ที่จัดเก็บข้อมูลไว้
- เมื่อ Lookup Service ส่ง Shard กลับมา ระบบจะ Query หรือ Update Shard นั้น

#### **ข้อดี**

Directory-based Sharding ใช้ Lookup Service แบบศูนย์กลางเพื่อติดตามว่าข้อมูลแต่ละส่วนถูกจัดเก็บไว้ที่ใด

- **การกระจายข้อมูลที่ยืดหยุ่น:** Directory-based Sharding รองรับการกระจายข้อมูลที่ยืดหยุ่น โดย Central Directory สามารถจัดการและอัปเดต Mapping ระหว่างข้อมูลกับตำแหน่งของ Shard ได้แบบ Dynamic
- **การ Routing Query อย่างมีประสิทธิภาพ:** Query สามารถถูกส่งไปยัง Shard ที่เหมาะสมได้อย่างมีประสิทธิภาพโดยใช้ข้อมูลที่จัดเก็บใน Directory ซึ่งช่วยเพิ่มประสิทธิภาพของ Query
- **Dynamic Scalability:** ระบบสามารถขยายหรือลดขนาดได้แบบ Dynamic ด้วยการเพิ่มหรือลบ Shard โดยไม่ต้องเปลี่ยนแปลง Application Logic

#### **ข้อเสีย**

แม้แนวทางนี้จะมีความยืดหยุ่น แต่ก็ทำให้ระบบต้องพึ่งพา Central Directory

- **จุดล้มเหลวแบบรวมศูนย์:** Central Directory เป็น Single Point of Failure หาก Directory ไม่พร้อมใช้งานหรือเกิดปัญหา อาจส่งผลกระทบต่อทั้งระบบ รวมถึงการเข้าถึงข้อมูลและการ Routing Query
- **Latency ที่เพิ่มขึ้น:** การ Routing Query ผ่าน Central Directory เพิ่มอีกหนึ่ง Layer ซึ่งอาจทำให้ Latency สูงขึ้นเมื่อเทียบกับกลยุทธ์ Sharding แบบอื่น

## **วิธีปรับ Database Sharding ให้กระจายข้อมูลอย่างสม่ำเสมอ**

ต่อไปนี้คือวิธีง่ายๆ ในการปรับ Database Sharding เพื่อให้กระจายข้อมูลได้อย่างสม่ำเสมอ:

- **ใช้ Consistent Hashing**: วิธีนี้ช่วยกระจายข้อมูลไปยัง Shard ทั้งหมดได้สม่ำเสมอมากขึ้น โดยใช้ Hashing Function ที่กำหนด Record ไปยัง Shard ต่างๆ ตามค่า Key ของ Record
- **เลือก Sharding Key ที่ดี**: การเลือก Sharding Key ที่สมดุลเป็นสิ่งสำคัญ Key ที่ไม่ก่อให้เกิด Hotspot จะช่วยให้ข้อมูลกระจายอย่างสม่ำเสมอไปยัง Server ทั้งหมด
- **ใช้ Range-Based Sharding อย่างระมัดระวัง**: หากใช้ Range-based Sharding ต้องกำหนดช่วงข้อมูลให้เหมาะสม เพื่อไม่ให้ Shard ใด Shard หนึ่งมีข้อมูลมากเกินไปเมื่อเทียบกับ Shard อื่น
- **Monitor และ Rebalance อย่างสม่ำเสมอ**: คอยตรวจสอบการกระจายข้อมูลและทำ Rebalance Shard เมื่อจำเป็น เพื่อหลีกเลี่ยงภาระงานที่ไม่สมดุลเมื่อข้อมูลเพิ่มขึ้น
- **ทำ Sharding Logic แบบอัตโนมัติ**: ใช้เครื่องมือ Automation หรือ Feature ที่มีมาในฐานข้อมูลเพื่อกระจายข้อมูลและจัดการ Sharding โดยอัตโนมัติ เพื่อรักษาสมดุลระหว่าง Shard

## **ทางเลือกอื่นแทน Database Sharding**

ต่อไปนี้คือทางเลือกบางส่วนที่สามารถใช้แทน Database Sharding ได้:

1. **Vertical Scaling**: [**Vertical Scaling**](https://www.geeksforgeeks.org/system-design/system-design-horizontal-and-vertical-scaling/) หมายถึงการอัปเกรด Server เดิมด้วยการเพิ่ม CPU, RAM หรือ Storage เพื่อรองรับภาระงานที่มากขึ้น แต่มีข้อจำกัดด้าน Hardware ที่แน่นอน จึงไม่สามารถขยายได้ตลอดไป
2. **Replication**: [**Replication**](https://www.geeksforgeeks.org/system-design/database-replication-and-their-types-in-system-design/) หมายถึงการสร้างสำเนาฐานข้อมูลบน Server หลายเครื่องเพื่อทำ Load Balancing และเพิ่ม High Availability แต่ Replica อาจพบปัญหาเรื่องการ Synchronization
3. **Partitioning**: [**Partitioning**](https://www.geeksforgeeks.org/system-design/data-partitioning-techniques/) หมายถึงการแบ่งข้อมูลออกเป็นส่วนย่อยภายใน Server เดียวกัน เพื่อเพิ่มประสิทธิภาพสำหรับชุดข้อมูลขนาดใหญ่โดยไม่ต้องใช้ Server หลายเครื่อง
4. **Caching**: [**Caching**](https://www.geeksforgeeks.org/system-design/caching-system-design-concept-for-beginners/) หมายถึงการจัดเก็บข้อมูลที่ถูกใช้งานบ่อยไว้ใน Redis/Memcached เพื่อลดภาระของฐานข้อมูลและเพิ่มความเร็วในการตอบสนอง
5. **CDNs**: [**CDNs**](https://www.geeksforgeeks.org/system-design/what-is-content-delivery-networkcdn-in-system-design/) หมายถึงการใช้ Content Delivery Network สำหรับข้อมูลที่มีการอ่านจำนวนมาก เพื่อลดการเข้าถึงฐานข้อมูลโดยตรงและส่งมอบ Content ได้เร็วขึ้น
