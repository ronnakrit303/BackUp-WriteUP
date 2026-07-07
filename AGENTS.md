# AGENTS.md

## ภาพรวมโปรเจกต์

โปรเจกต์นี้เป็นพื้นที่สำหรับเก็บและจัดทำ write-up ของงาน CompTIA A+ Core 1 and Core 2 CertMaster Perform โดยเน้นการจัดเก็บ Lab แต่ละหัวข้อให้เป็นระเบียบ มี README อธิบายขั้นตอนการทำ Lab และมีรูปภาพประกอบอยู่ในโฟลเดอร์ของแต่ละ Lab

โครงสร้างหลักของโปรเจกต์ตอนนี้คือ:

```text
CompTIA A+/
├── 6.2.7 Lab Configure IP Addresses/
│   ├── README.md
│   └── images/
├── 7.3.3 Lab Fix a Network Connection/
│   ├── README.md
│   └── images/
└── 7.4 Lab Troubleshoot a Network Issue/
    ├── README.md
    └── images/
```

## งานที่ทำไปแล้ว

### 1. สร้างโครงสร้างโฟลเดอร์

ได้สร้างโฟลเดอร์หลักชื่อ `CompTIA A+` สำหรับเก็บงานทั้งหมดของ CompTIA A+

ภายในโฟลเดอร์นี้ ได้สร้างโฟลเดอร์ Lab:

```text
6.2.7 Lab Configure IP Addresses
7.3.3 Lab Fix a Network Connection
7.4 Lab Troubleshoot a Network Issue
```

เหตุผลที่แยกเป็นโฟลเดอร์ Lab คือเพื่อให้แต่ละ Lab มี README และรูปภาพประกอบของตัวเอง ไม่ปะปนกับ Lab อื่น

### 2. สร้างโฟลเดอร์ images

ภายใน Lab `6.2.7 Lab Configure IP Addresses` ได้สร้างโฟลเดอร์:

```text
images
```

โฟลเดอร์นี้ใช้เก็บ screenshot ที่เกี่ยวข้องกับ Lab เช่น Exhibit, การตั้งค่า IPv4, ผล ping และผลคะแนน Lab

### 3. เขียน README.md สำหรับ Lab 6.2.7

ได้สร้างและเขียน `README.md` เป็นภาษาไทยสำหรับ Lab `6.2.7 Lab Configure IP Addresses`

เนื้อหาใน README ครอบคลุม:

1. ภาพรวมของ Lab
2. วัตถุประสงค์ของ Lab
3. สิ่งที่กำลังทำและเหตุผลที่ต้องทำ
4. ข้อมูลจาก Exhibit
5. ตารางค่าที่ใช้ตั้งค่า IPv4
6. วิธีคำนวณ IP address และ subnet mask
7. ขั้นตอนการตั้งค่า `Ethernet`
8. ขั้นตอนการตั้งค่า `Ethernet 2`
9. ขั้นตอนการทดสอบด้วยคำสั่ง `ping`
10. ขั้นตอนการตรวจคะแนน Lab
11. สรุปผลการทำ Lab

### 4. จัดการรูปภาพประกอบ

ได้คัดเลือกรูปภาพที่เหมาะสมจากหลายรูปที่มีเนื้อหาซ้ำกัน และเปลี่ยนชื่อไฟล์ให้เป็นระเบียบดังนี้:

```text
01-network-exhibit.png
02-ethernet-ipv4-config.png
03-ethernet2-ipv4-config.png
04-ping-preferred-dns.png
05-score-100.png
unused-exhibit-lab-view.png
```

รูปที่ใช้จริงใน README คือ:

1. `01-network-exhibit.png`
2. `02-ethernet-ipv4-config.png`
3. `03-ethernet2-ipv4-config.png`
4. `04-ping-preferred-dns.png`
5. `05-score-100.png`

ไฟล์ `unused-exhibit-lab-view.png` เป็นรูป Exhibit อีกเวอร์ชันหนึ่งที่ไม่ได้ใช้ใน README เพราะมีรูป Exhibit ที่อ่านง่ายกว่าอยู่แล้ว

### 5. แทรกรูปภาพใน README ตามขั้นตอนการทำ

รูปภาพไม่ได้ถูกแยกไว้เป็นหัวข้อหลักฐานท้ายไฟล์ แต่ถูกแทรกไว้ในขั้นตอนการทำ Lab โดยตรง เพื่อให้ผู้อ่านเห็นภาพประกอบในบริบทของแต่ละขั้นตอน

การจัดวางรูปใน README มีดังนี้:

1. รูป Exhibit อยู่ในขั้นตอนเปิด Exhibit
2. รูป Ethernet IPv4 อยู่ในขั้นตอนตั้งค่า Ethernet
3. รูป Ethernet 2 IPv4 อยู่ในขั้นตอนตั้งค่า Ethernet 2
4. รูป ping อยู่ในขั้นตอนทดสอบการเชื่อมต่อ
5. รูปคะแนน 100% อยู่ในขั้นตอนตรวจคะแนน Lab

### 6. เพิ่ม Lab 7.3.3 Fix a Network Connection

ได้สร้างโฟลเดอร์ `7.3.3 Lab Fix a Network Connection` ภายใต้ `CompTIA A+` พร้อมโฟลเดอร์ `images` และไฟล์ `README.md`

Lab นี้เป็นการ troubleshoot เครื่อง `Office1` ที่ไม่สามารถเชื่อมต่อ network และ internet ได้ โดยพบปัญหาทั้งฝั่ง hardware และ software configuration:

1. สาย network ไม่ได้เชื่อมต่อกับเครื่องอย่างถูกต้อง
2. เครื่องใช้ `Automatic (DHCP)` ทั้งที่ network ไม่มี DHCP server
3. เครื่องได้รับ APIPA address ขึ้นต้นด้วย `169.254.x.x`
4. DNS server เดิมไม่ถูกต้อง

ค่าที่ใช้แก้ไขใน Lab 7.3.3 คือ:

```text
IP address: 192.168.0.35
Subnet mask: 255.255.255.0
Default gateway: 192.168.0.5
Preferred DNS: 163.128.78.93
Alternate DNS: 163.128.80.93
```

ผลลัพธ์ของ Lab:

```text
Score: 100%
Plug the workstation into the network: Completed
Configure TCP/IP settings: Completed
```

### 7. จัดการรูปภาพประกอบสำหรับ Lab 7.3.3

ได้คัดเลือกรูปภาพที่สื่อความหมายดีที่สุดจากรูปที่มีเนื้อหาซ้ำกัน และเปลี่ยนชื่อไฟล์ให้เป็นลำดับตามขั้นตอนดังนี้:

```text
01-network-exhibit.png
02-ipconfig-media-disconnected.png
03-hardware-cable-connected.png
04-ethernet-before-apipa-dhcp.png
05-manual-ipv4-settings.png
06-ethernet-after-static-config.png
07-ipconfig-and-ping-success.png
08-score-100.png
unused-ethernet-after-static-config-full.png
unused-ethernet-before-cropped.png
unused-hardware-case-before-fix.png
unused-ipconfig-apipa-before-static.png
```

รูปที่ใช้จริงใน README คือรูปที่ขึ้นต้นด้วยเลข `01` ถึง `08` ส่วนรูปที่ขึ้นต้นด้วย `unused-` เป็นรูปที่เก็บไว้ในโฟลเดอร์ แต่ไม่ได้ใช้ใน README เพราะมีรูปอื่นที่อ่านง่ายกว่าหรือสื่อความหมายเดียวกันอยู่แล้ว

### 8. เพิ่ม Lab 7.4 Troubleshoot a Network Issue

ได้สร้างโฟลเดอร์ `7.4 Lab Troubleshoot a Network Issue` ภายใต้ `CompTIA A+` พร้อมโฟลเดอร์ `images` และไฟล์ `README.md`

Lab นี้เป็นการทำงานผ่านระบบ help desk ticket ชื่อ `Issue Trax` โดยต้องอ่าน ticket `#25` ที่แจ้งว่า laptop ใน `Office 2` ไม่สามารถเชื่อมต่อ `CorpNet wireless network` ได้ จากนั้นต้องตรวจสอบปัญหา แก้ไข เขียน comment ใน ticket และปิด ticket

สาเหตุของปัญหาใน Lab 7.4 คือ:

```text
Wireless switch บนตัว Office2-Lap อยู่ตำแหน่ง OFF
```

วิธีแก้ไขคือเปิด wireless switch เป็น `ON` แล้วเชื่อมต่อ laptop เข้ากับ `CorpNet`

ผลลัพธ์ของ Lab:

```text
Score: 100%
Connect the laptop in Office 2 to the CorpNet wireless network: Completed
```

### 9. จัดการรูปภาพประกอบสำหรับ Lab 7.4

ได้คัดเลือกรูปภาพที่สื่อความหมายดีที่สุดจากรูปที่มีเนื้อหาซ้ำกัน และเปลี่ยนชื่อไฟล์ให้เป็นลำดับตามขั้นตอนดังนี้:

```text
01-issue-trax-open-ticket-list.png
02-ticket-details-office2-laptop.png
03-itadmin-corpnet-connected.png
04-office2-laptop-no-wifi-option.png
05-wireless-switch-off.png
06-wireless-switch-on.png
07-office2-laptop-corpnet-connected.png
08-ticket-comment-and-closed.png
09-score-100.png
unused-floor-overview-office2.png
unused-itadmin-corpnet-before-connect.png
unused-office2-corpnet-before-connect.png
unused-office2-hardware-overview.png
unused-office2-laptop-desktop-before.png
unused-office2-wifi-available.png
```

รูปที่ใช้จริงใน README คือรูปที่ขึ้นต้นด้วยเลข `01` ถึง `09` ส่วนรูปที่ขึ้นต้นด้วย `unused-` เป็นรูปที่เก็บไว้ในโฟลเดอร์ แต่ไม่ได้ใช้ใน README เพราะมีรูปอื่นที่ชัดกว่า หรือสื่อขั้นตอนเดียวกันได้ครบกว่า

## สถานะปัจจุบัน

Lab `6.2.7 Lab Configure IP Addresses`, `7.3.3 Lab Fix a Network Connection` และ `7.4 Lab Troubleshoot a Network Issue` ทำเสร็จแล้ว และ README ของแต่ละ Lab ถูกจัดรูปแบบพร้อมใช้งานสำหรับเป็น write-up

ผลลัพธ์ของ Lab ที่บันทึกไว้:

```text
6.2.7 Score: 100%
7.3.3 Score: 100%
7.4 Score: 100%
```

## แนวทางสำหรับงานต่อไป

ถ้ามี Lab ใหม่ ควรสร้างโฟลเดอร์ใหม่ภายใต้ `CompTIA A+` โดยใช้ชื่อ Lab เป็นชื่อโฟลเดอร์ และจัดโครงสร้างภายในให้เหมือนกัน:

```text
CompTIA A+/
└── <Lab Name>/
    ├── README.md
    └── images/
```

README ของแต่ละ Lab ควรมี:

1. ชื่อ Lab
2. วัตถุประสงค์
3. ข้อมูลหรือค่าที่ต้องใช้
4. วิธีคำนวณถ้ามี
5. ขั้นตอนการทำแบบละเอียด
6. เหตุผลว่าทำไมต้องทำแต่ละขั้นตอน
7. รูปภาพประกอบในจุดที่เกี่ยวข้อง
8. สรุปผลลัพธ์สุดท้าย
