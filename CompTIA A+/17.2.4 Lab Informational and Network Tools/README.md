# 17.2.4 Lab: Informational and Network Tools

## ข้อมูลผู้ทำ Lab

- ชื่อ Lab: 17.2.4 Lab: Informational and Network Tools
- หัวข้อ: การใช้คำสั่งบน Linux เพื่อตรวจสอบเส้นทางเครือข่าย
- เครื่องที่ใช้งาน: IT-Laptop
- เครื่องมือที่ใช้: Terminal และคำสั่ง `traceroute`
- ผลลัพธ์สุดท้าย: ทำ Lab สำเร็จและได้คะแนน 100%

## ตอนนี้กำลังจะทำอะไร

ใน Lab นี้กำลังจะใช้เครื่อง Linux ชื่อ `IT-Laptop` เพื่อตรวจสอบว่าเครื่องใช้เส้นทางใดในการติดต่อไปยังเครื่องปลายทางบนเครือข่าย โดยจะใช้คำสั่ง `traceroute` เพื่อดูว่า packet เดินทางผ่าน router หรือ hop ใดบ้าง

เหตุผลที่ต้องทำแบบนี้ เพราะเครื่องมีอาการช้าเวลาเข้าถึง remote computer บน internet การดู route จะช่วยให้รู้ว่า traffic วิ่งผ่านอุปกรณ์ใดบ้าง และถ้ามีปัญหาระหว่างทางจะสามารถเริ่มวิเคราะห์ได้ว่าอาจเกิดจาก hop ใด

## วัตถุประสงค์

สิ่งที่ต้องทำใน Lab นี้มีดังนี้:

1. เปิด Exhibit เพื่อหา IP address ของ external DNS server
2. ตอบคำถามข้อ 1 จากข้อมูลใน Exhibit
3. ใช้คำสั่ง `traceroute` ไปยัง external DNS server
4. ตอบคำถามข้อ 2-5 จาก hop ที่ได้จาก `traceroute`
5. ใช้คำสั่ง `traceroute` ไปยัง remote computer `10.10.20.10`
6. ตอบคำถามข้อ 6-7 จากเส้นทางไปยัง remote computer
7. ตรวจคะแนนด้วย `Score Lab`

## คำสั่งที่ใช้ใน Lab

คำสั่งหลักที่ใช้คือ:

```bash
traceroute <destination>
```

ใน Lab นี้ใช้ 2 คำสั่ง:

```bash
traceroute 163.128.78.93
traceroute 10.10.20.10
```

`traceroute` ใช้สำหรับตรวจสอบเส้นทางจากเครื่องต้นทางไปยังปลายทาง โดยจะแสดง router แต่ละตัวที่ packet วิ่งผ่าน เรียกว่า hop

## ตารางคำตอบ

| ข้อ | คำถาม | คำตอบ |
| --- | --- | --- |
| Q1 | IP address ของ external DNS server คืออะไร | 163.128.78.93 |
| Q2 | IP address ของ default gateway หรือ hop 1 คืออะไร | 192.168.0.5 |
| Q3 | IP address ของ CorpNet main router หรือ hop 2 คืออะไร | 198.28.56.1 |
| Q4 | IP address ของ pfSense router หรือ hop 3 คืออะไร | 198.28.56.18 |
| Q5 | IP address ของ ISP internet router หรือ hop 4 คืออะไร | 198.28.2.254 |
| Q6 | มี router กี่ตัวใน path ระหว่าง Support กับ remote computer | 6 |
| Q7 | IP address ของ router ตัวสุดท้ายใน path คืออะไร | 73.44.216.7 |

## วิธีอ่านผลลัพธ์ traceroute

ตัวอย่างผลลัพธ์ของ `traceroute` จะมีลักษณะคล้าย ๆ นี้:

```text
1  192.168.0.5
2  198.28.56.1
3  198.28.56.18
4  198.28.2.254
```

เลขด้านหน้าคือหมายเลข hop ส่วน IP address ด้านหลังคือ router หรืออุปกรณ์เครือข่ายที่ packet ผ่านในแต่ละลำดับ

เช่น:

- hop 1 คือ router ตัวแรกที่เครื่องส่งข้อมูลออกไปหา
- hop 2 คือ router ตัวถัดไปหลังจาก default gateway
- hop สุดท้ายก่อนถึงปลายทางช่วยบอกว่า traffic วิ่งออกไปทาง router ใดก่อนถึงเครื่องปลายทาง

## ขั้นตอนการทำ Lab

### ขั้นตอนที่ 1: เข้าเครื่อง IT-Laptop

1. เปิด Lab `17.2.4 Lab: Informational and Network Tools`
2. เข้าเครื่อง Linux ชื่อ `IT-Laptop`
3. รอให้เข้า desktop ของ Linux ให้เรียบร้อย

เหตุผลที่ต้องทำบน `IT-Laptop` เพราะโจทย์ระบุว่าเครื่อง Linux นี้เป็นเครื่องที่มีปัญหาเข้าถึง remote computer ช้า จึงต้องตรวจสอบ route จากเครื่องนี้โดยตรง

### ขั้นตอนที่ 2: เปิด Questions และ Exhibits

1. ที่มุมขวาบนของ Lab กด `Questions`
2. เปิดหน้าคำถาม Q1-Q7 ไว้
3. กด `Exhibits`
4. ดูแผนผัง network
5. หา section ที่ชื่อ `External DNS Servers`

จาก Exhibit จะได้ external DNS server เป็น:

```text
163.128.78.93
```

นำค่านี้ไปตอบ Q1

เหตุผลที่ต้องดู Exhibit ก่อน เพราะโจทย์ไม่ได้ให้ IP ของ external DNS server ในคำสั่งโดยตรง แต่ให้ผู้ทำ Lab หาเองจากแผนผังเครือข่าย

### ขั้นตอนที่ 3: เปิด Terminal

1. จาก Favorites bar ด้านซ้าย เลือก `Terminal`
2. ถ้า Terminal ยังไม่เปิด ให้ไปที่เมนู `Application` แล้วเลือก Terminal
3. รอจนเห็น command prompt

เหตุผลที่ต้องใช้ Terminal เพราะ Lab นี้ต้องใช้คำสั่ง network troubleshooting บน Linux

### ขั้นตอนที่ 4: ใช้ traceroute ไปยัง external DNS server

ใน Terminal ให้พิมพ์คำสั่ง:

```bash
traceroute 163.128.78.93
```

จากนั้นกด `Enter`

ผลลัพธ์ที่ได้จะใช้ตอบคำถาม Q2-Q5

คำตอบคือ:

```text
Q2: 192.168.0.5
Q3: 198.28.56.1
Q4: 198.28.56.18
Q5: 198.28.2.254
```

ความหมายของแต่ละ hop:

```text
Hop 1: Default gateway = 192.168.0.5
Hop 2: CorpNet main router = 198.28.56.1
Hop 3: pfSense router = 198.28.56.18
Hop 4: ISP internet router = 198.28.2.254
```

เหตุผลที่ต้องรัน `traceroute 163.128.78.93` เพราะต้องการดู route จากเครื่อง `IT-Laptop` ไปยัง external DNS server และใช้ hop ที่แสดงออกมาตอบคำถามของ Lab

### ขั้นตอนที่ 5: ตอบคำถาม Q1-Q5

ในหน้า `Questions` ให้ตอบ:

```text
Q1: 163.128.78.93
Q2: 192.168.0.5
Q3: 198.28.56.1
Q4: 198.28.56.18
Q5: 198.28.2.254
```

ก่อนตอบให้ตรวจสอบว่าพิมพ์ IP ถูกต้องครบทุก octet เพราะถ้าพิมพ์ผิดเพียงตัวเดียว Lab จะให้คะแนนผิดทันที

### ขั้นตอนที่ 6: ใช้ traceroute ไปยัง remote computer

โจทย์กำหนด remote computer เป็น IP:

```text
10.10.20.10
```

ใน Terminal ให้พิมพ์:

```bash
traceroute 10.10.20.10
```

จากนั้นกด `Enter`

ใช้ผลลัพธ์ที่ได้ตอบคำถาม Q6 และ Q7

คำตอบคือ:

```text
Q6: 6
Q7: 73.44.216.7
```

เหตุผลที่ Q6 ตอบ `6` เพราะ route ระหว่าง Support กับ remote computer มี router ทั้งหมด 6 ตัวใน path

เหตุผลที่ Q7 ตอบ `73.44.216.7` เพราะเป็น IP address ของ router ตัวสุดท้ายใน path ก่อนถึง remote computer

### ขั้นตอนที่ 7: ตอบคำถาม Q6-Q7

ในหน้า `Questions` ให้ตอบ:

```text
Q6: 6
Q7: 73.44.216.7
```

ถ้า Q6 เป็นช่องแบบ drop-down ให้เลือก `6`

ถ้า Q7 เป็นช่องแบบ drop-down หรือช่องกรอก ให้เลือกหรือกรอก:

```text
73.44.216.7
```

### ขั้นตอนที่ 8: ตรวจคำตอบทั้งหมดก่อน Score Lab

ตรวจคำตอบทั้งหมดอีกครั้ง:

```text
Q1: 163.128.78.93
Q2: 192.168.0.5
Q3: 198.28.56.1
Q4: 198.28.56.18
Q5: 198.28.2.254
Q6: 6
Q7: 73.44.216.7
```

เหตุผลที่ควรตรวจซ้ำ เพราะ Lab นี้เป็นการตอบคำถามจากข้อมูล command output ถ้ากรอก IP ผิดตำแหน่งหรือสะกดผิดจะเสียคะแนน

### ขั้นตอนที่ 9: ตรวจคะแนน Lab

1. กด `Score Lab`
2. ตรวจสอบว่า required actions ผ่านครบ

ผลลัพธ์ที่ถูกต้องควรเป็น:

```text
Score: 100%
Run traceroute to find the route to the external DNS server: Completed
Run traceroute to find the route to 10.10.20.10: Completed
Q1-Q7: Correct
```

## รูปภาพที่ควรถ่ายสำหรับ Write-up

ตอนนี้โฟลเดอร์ `images` ยังไม่มีรูปภาพประกอบ ถ้าจะเก็บหลักฐานสำหรับ README แนะนำให้ถ่ายรูปประมาณนี้:

1. รูป Exhibit ที่เห็น external DNS server
2. รูป Terminal หลังรัน `traceroute 163.128.78.93`
3. รูป Terminal หลังรัน `traceroute 10.10.20.10`
4. รูปหน้า Questions ที่ตอบครบ
5. รูป Score 100%

เมื่อมีรูปแล้วสามารถนำมาใส่ในโฟลเดอร์ `images` แล้วตั้งชื่อเป็นลำดับ เช่น:

```text
01-external-dns-exhibit.png
02-traceroute-external-dns.png
03-traceroute-remote-computer.png
04-questions-answered.png
05-score-100.png
```

## จุดที่ต้องระวัง

- ต้องใช้คำสั่ง `traceroute` ไม่ใช่ `ping`
- Q1 ต้องตอบ external DNS server จาก Exhibit คือ `163.128.78.93`
- Q2-Q5 ต้องอ้างอิงจาก hop ของ `traceroute 163.128.78.93`
- Q6-Q7 ต้องอ้างอิงจาก `traceroute 10.10.20.10`
- IP address ต้องพิมพ์ให้ถูกทุกตัว
- ถ้า command output แสดงหลายบรรทัด ให้ดูหมายเลข hop ให้ตรงกับคำถาม

## สรุปผล

ใน Lab นี้ได้ใช้เครื่อง Linux `IT-Laptop` เปิด Terminal แล้วใช้คำสั่ง `traceroute` เพื่อตรวจสอบเส้นทาง network ไปยัง external DNS server และ remote computer

จากการตรวจสอบ route ไปยัง external DNS server พบว่า hop 1 คือ default gateway `192.168.0.5`, hop 2 คือ CorpNet main router `198.28.56.1`, hop 3 คือ pfSense router `198.28.56.18` และ hop 4 คือ ISP internet router `198.28.2.254`

จากการตรวจสอบ route ไปยัง remote computer `10.10.20.10` พบว่า path มี router ทั้งหมด 6 ตัว และ router ตัวสุดท้ายใน path คือ `73.44.216.7` เมื่อตอบคำถามครบและกด `Score Lab` ได้คะแนน `100%`
