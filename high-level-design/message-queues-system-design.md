# **Message Queues - การออกแบบระบบ**

Message Queue ช่วยให้ส่วนประกอบต่างๆ ของระบบสามารถสื่อสารกันแบบอะซิงโครนัสได้ โดยทำหน้าที่เป็นบัฟเฟอร์ระหว่าง Producer และ Consumer ช่วยแยกการทำงานของบริการออกจากกัน ทำให้แต่ละส่วนสามารถทำงานได้อย่างอิสระและเชื่อถือได้ แม้จะเกิดความล่าช้าหรือความล้มเหลว

- ช่วยเพิ่มความสามารถในการขยายระบบและรองรับโหลด โดยกระจายงานไปยัง Consumer หลายตัว
- เพิ่มความทนทานต่อความล้มเหลวด้วยการเก็บข้อความไว้จนกว่าจะถูกประมวลผล

> **ตัวอย่าง:** ในระบบอีคอมเมิร์ซ เมื่อผู้ใช้สั่งซื้อสินค้า Order Service จะส่งข้อความไปยัง Queue จากนั้นบริการอื่นๆ เช่น Payment Service และ Notification Service จะประมวลผลข้อความแบบอะซิงโครนัส โดยไม่ทำให้คำขอของผู้ใช้ต้องรอ

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20250930085200425394/message_queue_-660.webp" alt="message_queue_" />

> ลองนึกถึงร้านพิซซ่าร้านโปรดของคุณ ที่มีทั้งการทำและจัดส่งพิซซ่า เบื้องหลังมีระบบหนึ่งที่ช่วยให้ทุกอย่างดำเนินไปอย่างราบรื่น ระบบนี้เรียกว่า Message Queue ซึ่งเปรียบเสมือนรายการสิ่งที่ต้องทำแบบพิเศษที่ช่วยให้พ่อครัวและพนักงานจัดส่งรู้ว่าต้องทำพิซซ่าอะไรและนำไปส่งที่ไหน

โครงสร้างของข้อความโดยทั่วไปประกอบด้วยสองส่วนหลัก:

- **Headers:** เก็บ Metadata ของข้อความ เช่น ตัวระบุที่ไม่ซ้ำกัน Timestamp ประเภทของข้อความ และข้อมูลสำหรับการกำหนดเส้นทาง
- **Body:** เก็บ Payload หรือเนื้อหาจริงของข้อความ ซึ่งสามารถอยู่ในรูปแบบใดก็ได้ เช่น ข้อความ ข้อมูลไบนารี หรือข้อมูลที่มีโครงสร้างอย่าง JSON

## **ส่วนประกอบ**

ระบบ Message Queue ประกอบด้วยส่วนประกอบต่างๆ ที่ทำงานร่วมกันเพื่อส่ง จัดเก็บ และประมวลผลข้อความแบบอะซิงโครนัส

- **Message Producer:** Message Producer ทำหน้าที่สร้างข้อความและส่งข้อความไปยัง Message Queue ซึ่งอาจเป็นโปรแกรมหรือส่วนใดส่วนหนึ่งของระบบที่สร้างข้อมูลเพื่อนำไปใช้งานร่วมกัน
- **Message Queue:** ข้อความจะถูกจัดเก็บและจัดการโดยโครงสร้างข้อมูลหรือบริการที่เรียกว่า Message Queue จนกว่า Message Consumer จะนำข้อความไปใช้งาน โดยทำหน้าที่เป็นตัวกลางหรือบัฟเฟอร์ระหว่าง Producer และ Consumer
- **Message Consumer:** Message Consumer ทำหน้าที่ดึงข้อความจาก Message Queue และนำไปประมวลผล โดย Consumer หลายตัวสามารถอ่านข้อความจาก Queue พร้อมกันได้
- **Message Broker (ไม่บังคับ):** ในระบบ Message Queue บางประเภท Message Broker จะทำหน้าที่เป็นตัวกลางระหว่าง Producer และ Consumer พร้อมความสามารถเพิ่มเติม เช่น การกำหนดเส้นทางข้อความ การกรองข้อความ และการแปลงรูปแบบข้อความ

## **การทำงาน**

ขั้นตอนในการทำความเข้าใจว่า Message Queue ทำงานอย่างไร:

- **ขั้นตอนที่ 1: การส่งข้อความ:** Message Producer สร้างข้อความและส่งไปยัง Message Queue โดยทั่วไปข้อความจะมีข้อมูลหรือคำสั่งที่ต้องนำไปประมวลผลหรือสื่อสารต่อ
- **ขั้นตอนที่ 2: การนำข้อความเข้าคิว:** Message Queue จะจัดเก็บข้อความไว้ชั่วคราวเพื่อให้ Consumer หนึ่งตัวหรือหลายตัวสามารถนำไปใช้งานได้ โดยทั่วไปข้อความจะถูกจัดเก็บตามลำดับเข้าก่อนออกก่อน (FIFO)
- **ขั้นตอนที่ 3: การรับข้อความไปประมวลผล:** Message Consumer จะดึงข้อความจาก Queue เมื่อพร้อมประมวลผล และสามารถทำงานตามจังหวะของตนเองได้ ซึ่งช่วยให้เกิดการสื่อสารแบบอะซิงโครนัส
- **ขั้นตอนที่ 4: การตอบรับ (ไม่บังคับ):** ในระบบ Message Queue บางประเภท Consumer สามารถส่ง Acknowledgment กลับไปยัง Queue เพื่อระบุว่าข้อความถูกประมวลผลสำเร็จแล้ว ซึ่งมีความสำคัญต่อการรับประกันการส่งข้อความและป้องกันข้อความสูญหาย

> **ตัวอย่าง**: ตัวอย่างง่ายๆ ของ Message Queue คือกล่องจดหมายอีเมล เมื่อคุณส่งอีเมล อีเมลจะถูกนำไปวางไว้ในกล่องจดหมายของผู้รับ จากนั้นผู้รับสามารถเปิดอ่านได้เมื่อสะดวก กล่องจดหมายนี้จึงทำหน้าที่เป็นบัฟเฟอร์ระหว่างผู้ส่งและผู้รับ และช่วยแยกการทำงานของทั้งสองออกจากกัน

## **ความสำคัญ**

Message Queue มีความจำเป็นสำหรับการจัดการความท้าทายหลายประการใน [ระบบแบบกระจาย](https://www.geeksforgeeks.org/computer-networks/what-is-a-distributed-system/) ได้แก่:

- **การสื่อสารแบบอะซิงโครนัส:** Message Queue ช่วยให้แอปพลิเคชันสามารถส่งและรับข้อความได้โดยไม่ต้องรอการตอบกลับ ซึ่งเป็นสิ่งสำคัญสำหรับการสร้างระบบที่รองรับการขยายและมีความน่าเชื่อถือ
- **การแยกส่วนการทำงาน:** Message Queue ช่วยแยกแอปพลิเคชันออกจากกัน ทำให้สามารถพัฒนาแต่ละส่วนได้อย่างอิสระ ส่งผลให้ระบบมีความยืดหยุ่นและดูแลรักษาได้ง่ายขึ้น
- **ความสามารถในการขยายระบบ:** Message Queue สามารถขยายเพื่อรองรับข้อความจำนวนมากได้ด้วยการเพิ่มเซิร์ฟเวอร์ จึงเหมาะสำหรับแอปพลิเคชันที่มีปริมาณทราฟฟิกสูง
- **ความน่าเชื่อถือ:** Message Queue สามารถออกแบบให้มีความน่าเชื่อถือสูงได้ด้วยความสามารถอย่างการจัดเก็บข้อความแบบถาวร การลองใหม่ และ Dead Letter Queue ซึ่งช่วยให้มั่นใจว่าข้อความจะไม่สูญหายแม้เกิดความล้มเหลว
- **การจัดการ Workflow:** Message Queue สามารถใช้สร้าง Workflow ที่ซับซ้อน เช่น การประมวลผลคำสั่งซื้อและการชำระเงิน ซึ่งช่วยเพิ่มประสิทธิภาพและความถูกต้องของกระบวนการเหล่านี้

## **ประเภท**

Message Queue ในการออกแบบระบบมีสองประเภทหลัก:

### **1. Point-to-Point Message Queues**

Point-to-Point Message Queue จะจัดเก็บข้อความที่ Producer ส่งเข้ามาไว้จนกว่า Consumer จะดึงไปใช้งาน เมื่อข้อความถูก Consumer รับไปแล้ว ข้อความจะถูกลบออกจาก Queue และ Consumer อื่นจะไม่สามารถประมวลผลข้อความนั้นได้อีก

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20260330182849095324/queue-660.webp" alt="Point-to-point Message Queues" />

Point-to-Point Message Queue สามารถนำไปใช้สร้างรูปแบบการทำงานต่างๆ เช่น:

- **Request-Response:** Producer ส่งข้อความ Request ไปยัง Queue จากนั้น Consumer ดึงข้อความไปประมวลผลและส่งข้อความ Response กลับมา
- **Work Queue:** Producer ส่งงานไปยัง Queue และ Consumer ดึงงานเหล่านั้นไปประมวลผล
- **Guaranteed Delivery:** Producer ส่งข้อความไปยัง Queue และสามารถกำหนดให้ Consumer พยายามดึงข้อความซ้ำจนกว่าจะประมวลผลสำเร็จ

### **2. Publish-Subscribe Message Queues**

Publish-Subscribe Message Queue จะส่งข้อความจาก Producer ไปยัง Consumer ทุกตัวที่ Subscribe อยู่ Consumer สามารถ Subscribe หลาย Queue และ Unsubscribe ได้ทุกเมื่อ ทำให้การจัดการข้อความมีความยืดหยุ่น

- Publish-Subscribe Message Queue มักใช้สร้างแอปพลิเคชัน Streaming แบบ Real-Time เช่น โซเชียลมีเดียและตัวแสดงราคาหุ้นแบบเรียลไทม์
- นอกจากนี้ยังสามารถใช้สร้าง Event-Driven Architecture ซึ่งส่วนประกอบต่างๆ ของระบบสื่อสารกันด้วยการ Publish และ Subscribe Event

## **การกำหนดเส้นทางข้อความ**

Message Routing คือการกำหนดว่าข้อความจะถูกส่งไปยังผู้รับที่ต้องการอย่างไร โดยสามารถใช้วิธีต่อไปนี้:

- **Topic-Based Routing:** ข้อความจะถูกส่งไปยัง Topic หรือ Channel และ Subscriber จะระบุ Topic ที่สนใจ จากนั้นข้อความจะถูกส่งไปยัง Subscriber ทุกตัวของ Topic นั้น
- **Direct Routing:** ข้อความจะถูกส่งโดยตรงไปยัง Queue หรือ Consumer ที่กำหนดตาม Address หรือ Routing Key
- **Content-Based Routing:** การตัดสินใจกำหนดเส้นทางจะอ้างอิงจากเนื้อหาของข้อความ โดยกำหนด Filter หรือ Rule เพื่อส่งข้อความที่ตรงตามเงื่อนไขที่ระบุ

## **ความสามารถในการขยายระบบ**

[ความสามารถในการขยายระบบ](https://www.geeksforgeeks.org/system-design/what-is-scalability/) มีความสำคัญเพื่อให้ระบบ Message Queue สามารถรองรับโหลดที่เพิ่มขึ้นได้อย่างมีประสิทธิภาพ โดยสามารถทำได้ดังนี้:

- **Distributed Queues:** สร้าง Message Queue เป็นระบบแบบกระจายที่มีหลาย Node เพื่อรองรับการขยายระบบในแนวนอน
- **Partitioning:** แบ่ง Queue ออกเป็น Partition เพื่อกระจายการประมวลผลข้อความไปยัง Node หรือ Cluster ต่างๆ
- **Load Balancing:** ใช้ [Load Balancer](https://www.geeksforgeeks.org/system-design/what-is-load-balancer-system-design/) เพื่อกระจายข้อความขาเข้าไปยัง Queue Consumer อย่างสม่ำเสมอ

## **Dead Letter Queues และการจัดลำดับความสำคัญของข้อความ**

แนวคิดเหล่านี้ช่วยจัดการข้อความที่ประมวลผลไม่สำเร็จ และควบคุมลำดับการประมวลผลข้อความภายในระบบ

### **1. Dead Letter Queues**

Dead Letter Queue (DLQ) เป็นกลไกสำหรับจัดการข้อความที่ไม่สามารถประมวลผลได้สำเร็จ ซึ่งรวมถึง:

- ข้อความที่มีข้อผิดพลาดในเนื้อหาหรือรูปแบบ
- ข้อความที่เกิน Time-to-Live (TTL) หรือจำนวนครั้งในการพยายามส่ง
- ข้อความที่ไม่สามารถส่งไปยัง Consumer ใดได้

DLQ ช่วยให้สามารถตรวจสอบและอาจนำข้อความที่ล้มเหลวกลับมาประมวลผลใหม่ได้ โดยไม่ปล่อยให้ข้อความเหล่านั้นไปขัดขวางการทำงานของระบบ

### **2. การจัดลำดับความสำคัญของข้อความ**

Message Prioritization คือกระบวนการกำหนดระดับความสำคัญให้กับข้อความเพื่อควบคุมลำดับการประมวลผล โดยเกณฑ์ในการจัดลำดับความสำคัญอาจประกอบด้วย:

- **ความเร่งด่วน:** ข้อความที่มีความสำคัญสูงกว่าอาจต้องถูกประมวลผลก่อนข้อความที่มีความสำคัญต่ำกว่า
- **เนื้อหาของข้อความ:** ข้อความที่มีข้อมูลหรือคำสั่งสำคัญอาจได้รับลำดับความสำคัญสูงกว่า
- **กฎทางธุรกิจ:** สามารถใช้กฎทางธุรกิจหรืออัลกอริทึมที่กำหนดเองเพื่อตัดสินลำดับความสำคัญของข้อความ

## **การนำ Message Queue ไปใช้งาน**

Message Queue สามารถนำไปใช้งานได้หลายรูปแบบ แต่โดยทั่วไปจะเป็นไปตามรูปแบบง่ายๆ ดังนี้:

- **Producer:** แอปพลิเคชันที่ส่งข้อความไปยัง Queue
- **Message Broker:** เซิร์ฟเวอร์ที่จัดเก็บและส่งต่อข้อความระหว่าง Producer และ Consumer
- **Consumer:** แอปพลิเคชันที่รับข้อความจาก Queue

**โจทย์:**

> ในสถานการณ์จริง คุณอาจพิจารณาใช้บริการ Message Queue โดยเฉพาะ เช่น RabbitMQ หรือ Apace Kafka สำหรับระบบแบบกระจาย

ต่อไปนี้คือคำแนะนำทีละขั้นตอนสำหรับการสร้าง Message Queue พื้นฐานด้วย C++:

### **ขั้นตอนที่ 1: กำหนดโครงสร้างข้อความ:**

เริ่มต้นด้วยการกำหนดโครงสร้างของข้อความ โครงสร้างนี้ควรประกอบด้วยข้อมูลที่จำเป็นสำหรับการสื่อสารระหว่างส่วนต่างๆ ของระบบ

```jsx
class Message {
    constructor(messageType, payload) {
        this.messageType = messageType;
        this.payload = payload;
    }
    // Add any other fields as needed
}
```

### **ขั้นตอนที่ 2: สร้าง Message Queue:**

สร้าง Class สำหรับ Message Queue โดย Class นี้ควรรองรับการทำงาน เช่น Enqueue และ Dequeue

```jsx
class MessageQueue {
    constructor() {
        this.queue = [];
        this.mutex = new Promise(resolve => this.resolveMutex = resolve);
    }

    // Enqueue a message
    async enqueue(message) {
        await this.mutex;
        try {
            this.queue.push(message);
        } finally {
            this.resolveMutex();
        }
    }

    // Dequeue a message
    async dequeue() {
        await this.mutex;
        try {
            while (this.queue.length === 0) {
                await new Promise(resolve => this.resolveWait = resolve);
            }
            return this.queue.shift();
        } finally {
            this.resolveMutex();
        }
    }
}
```

### **ขั้นตอนที่ 3: สร้าง Producer และ Consumer**

สร้าง Function หรือ Class ที่ทำหน้าที่เป็น Producer และ Consumer โดย Producer จะ Enqueue ข้อความ และ Consumer จะ Dequeue ข้อความ

```jsx
// Producer function
function producer(messageQueue, messageType, payload) {
    let message = { messageType: messageType, payload: payload };

    messageQueue.enqueue(message);
}

// Consumer function
function consumer(messageQueue) {
    while (true) {
        let message = messageQueue.dequeue();
        // Process the message
        // ...
    }
}
```

### **ขั้นตอนที่ 4: ใช้งาน Message Queue**

สร้าง Instance ของ Message Queue, Producer และ Consumer แล้วนำไปใช้ในโปรแกรม

```jsx
class MessageQueue {
    constructor() {
        this.queue = [];
        this.waiting = [];
    }

    // Producer sends a message
    async send(message) {
        if (this.waiting.length > 0) {
            // If a consumer is waiting, resolve it immediately
            const resolve = this.waiting.shift();
            resolve(message);
        } else {
            // Otherwise, push message to queue
            this.queue.push(message);
        }
    }

    // Consumer receives a message
    receive() {
        return new Promise((resolve) => {
            if (this.queue.length > 0) {
                // If a message is available, resolve immediately
                resolve(this.queue.shift());
            } else {
                // Otherwise, wait until a message is available
                this.waiting.push(resolve);
            }
        });
    }
}

// Producer function
async function producer(mq, id, message) {
    console.log(`Producer ${id} sending: ${message}`);
    await mq.send(message);
}

// Consumer function
async function consumer(mq) {
    const msg = await mq.receive();
    console.log(`Consumer received: ${msg}`);
}

// Main thread logic
(async () => {
    const messageQueue = new MessageQueue();

    // Start consumer first (to simulate waiting)
    consumer(messageQueue);

    // Simulate delay before sending
    setTimeout(() => {
        producer(messageQueue, 1, 'Hello, World!');
    }, 1000);
})();
```

**ผลลัพธ์**

```
Producer 1 sending: Hello, World!
Consumer received: Hello, World!
```
