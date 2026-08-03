# Journey Log Book - CompTIA A+ Week 1

## ภาพรวม Log Book

Log Book นี้เป็นการจด journey ของผมในค่ายว่าแต่ละช่วงได้เรียนรู้อะไร เจอปัญหาอะไร แก้ปัญหายังไง และได้อะไรกลับมาจากการแก้ปัญหาเหล่านั้น

ภาพรวมของค่ายแบ่งเป็น 3 week:

```text
Week 1: CompTIA A+
Week 2: TryHackMe
Week 3: Root the Box
```

ไฟล์นี้จะเขียนเฉพาะ `Week 1: CompTIA A+` ก่อน ส่วน Week 2 และ Week 3 จะเขียนเพิ่มภายหลัง

## Week 1: CompTIA A+

Week 1 เป็นช่วงที่ผมได้เรียนพื้นฐานงาน IT support และ security ฝั่ง Windows เป็นหลัก ตั้งแต่ network เบื้องต้น, account และ permission, endpoint security, remote access, Linux, scripting ไปจนถึง incident response และการทำงานผ่าน ticket

สิ่งที่ผมรู้สึกว่าเป็นแกนหลักของ Week นี้คือ “การแก้ปัญหาแบบมีเหตุผล” ไม่ใช่แค่กดตามขั้นตอนให้ผ่าน Lab แต่ต้องเข้าใจว่าทำไมต้องตั้งค่านี้ ทำไมต้องตรวจจุดนี้ และทำไมต้องเก็บหลักฐานหรือ update ticket หลังแก้ปัญหาเสร็จ

## ตารางหัวข้อที่เรียนใน Week 1

| Day | Topic | Focused Labs |
| --- | --- | --- |
| Day 1 | Networking Basics | Lab 6.2.7 Configure IP Addresses, Lab 7.3.3 Fix a Network Connection, Lab 7.4 Troubleshoot a Network Issue, Lab 13.3.9 Local Firewall Settings |
| Day 2 | Windows Identity & Access Control | Lab 15.1.8 Create User Accounts, Lab 15.2.6 Group Policy Management, Lab 15.3.6 Configure NTFS Permissions, Lab 19.1.2 Enforce Password Settings |
| Day 3 | Endpoint Defense & Malware Response | Lab 18.1.3 Respond to Social Engineering Exploits, Lab 19.2.7 Configure Microsoft Defender Antivirus, Lab 19.2.14 Analyze Workstation Security Settings, Lab 19.5 Resolve Security Tickets |
| Day 4 | Remote Access, Monitoring & Linux | Lab 13.3.7 Configure a VPN Connection, Lab 14.3.10 Manage Applications, Lab 17.2.4 Informational and Network Tools, Lab 17.2.6 Configure Linux |
| Day 5 | Scripting, IR & Documentation | Lab 22.3.10 Live Lab: Implement a PowerShell Script, Lab 22.3.11 Live Lab: Implement a Bash Script, Lab 21.4 Challenge Live Lab: Resolve Incident Response Tickets, Lab 11.1.13 / 11.1.14 Create a Ticket / Close a Ticket |

หมายเหตุ: ตอนนี้ผมทำ write-up ละเอียดไว้ถึง Day 1-Day 3 ส่วน Day 4 และ Day 5 ยังไม่ได้เขียน README แยกเต็ม ๆ แต่ยังใส่ใน journey นี้ไว้ เพราะเป็นส่วนหนึ่งของเนื้อหาที่เรียนในค่าย

## Day 1: Networking Basics

### ได้เรียนรู้อะไร

Day 1 ทำให้ผมเข้าใจพื้นฐาน network มากขึ้น โดยเฉพาะเรื่อง IPv4, subnet mask, default gateway, DNS, firewall profile และการ troubleshoot ปัญหา network แบบไล่จากง่ายไปยาก

ใน Lab 6.2.7 ผมได้ฝึกตั้งค่า IP address แบบ manual/static ให้ network adapter สองตัว และได้คำนวณ IP จาก subnet เช่น `192.168.0.0/24` ต้องใช้ subnet mask `255.255.255.0` และ last valid IP คือ `192.168.0.254` ส่วน `10.0.0.0/16` ใช้ subnet mask `255.255.0.0` และ last valid IP คือ `10.0.255.254`

ใน Lab 7.3.3 ผมได้เห็นว่าปัญหา network ไม่ได้มีแค่เรื่อง IP อย่างเดียว แต่มีทั้งสาย LAN ที่เสียบไม่ถูกต้อง, adapter disconnected, เครื่องได้ APIPA address ขึ้นต้นด้วย `169.254.x.x`, ไม่มี DHCP server และต้องแก้ด้วยการตั้ง IPv4 แบบ static

ใน Lab 7.4 ผมได้เรียนว่าบางครั้งปัญหา network ไม่ได้อยู่ใน Windows setting แต่อยู่ที่ hardware เช่น wireless switch ของ laptop ถูกปิดอยู่ ทำให้ Windows ไม่แสดง Wi-Fi network ให้เชื่อมต่อ

ใน Lab 13.3.9 ผมได้เรียนเรื่อง Windows Firewall profile โดยเฉพาะ `Public network profile` และเข้าใจว่าการ allow app ผ่าน firewall ควรทำเท่าที่จำเป็น เพื่อลด attack surface

### ปัญหาที่เจอ

ปัญหาแรกคือผมยังสับสนเรื่องการคำนวณ IP address เช่น last valid address คืออะไร ทำไม `192.168.0.255` ใช้ไม่ได้ และทำไม `Ethernet 2` ไม่ต้องใส่ default gateway

อีกปัญหาคือในบาง Lab คำสั่งหรือเมนูบางอย่างใน simulation ใช้ไม่ได้ เช่นเปิด `cmd` ด้วยวิธีเดิมไม่ได้ ทำให้ตอนแรกงงว่าต้องตรวจ ping ยังไง

นอกจากนี้ใน Lab 7.3.3 ผมเจอปัญหาที่ต้องแก้ทั้ง hardware และ software พร้อมกัน ตอนแรก ping ไม่ผ่าน เพราะสาย LAN ยังไม่ได้เชื่อมต่อ และ IP configuration ยังผิดอยู่

### แก้ปัญหายังไง

ผมแก้เรื่อง subnet โดยกลับไปดู Exhibit และไล่คิดจาก network address, usable IP range และ broadcast address เช่น `/24` มีช่วง usable เป็น `.1` ถึง `.254` ดังนั้น last valid address คือ `.254` ไม่ใช่ `.255`

เรื่อง default gateway ผมเข้าใจเพิ่มว่า gateway ใช้สำหรับออกไปเครือข่ายอื่นหรือ internet ดังนั้น adapter ที่ไม่ได้ใช้เชื่อมต่อออกนอก network จึงไม่ควรใส่ gateway

เรื่อง command ที่เปิดไม่ได้ ผมเปลี่ยนไปใช้ Windows Terminal หรือ PowerShell ตามที่ Lab รองรับ แล้วใช้ `ping` เพื่อทดสอบการเชื่อมต่อแทน

สำหรับปัญหา hardware ผมเริ่มไล่จากสิ่งที่มองเห็นก่อน เช่นสาย LAN เสียบถูก port หรือไม่, adapter มีสถานะ connected หรือไม่ แล้วค่อยไปแก้ IP address, DNS และ default gateway

### ได้อะไรจากการแก้ปัญหา

ผมได้เรียนว่าการ troubleshoot network ควรไล่เป็นลำดับ ไม่ควรกระโดดไปแก้ DNS หรือ firewall ทันทีถ้ายังไม่รู้ว่าสายเสียบอยู่หรือเปล่า

สิ่งที่ได้ชัดที่สุดคือ network troubleshooting ควรเริ่มจาก:

```text
Physical connection -> IP address -> Subnet mask -> Gateway -> DNS -> Firewall -> Ping test
```

Day 1 ทำให้ผมเริ่มมอง network เป็นระบบมากขึ้น ไม่ใช่แค่จำว่า IP ต้องใส่อะไร แต่เริ่มเข้าใจว่าค่าแต่ละตัวมีหน้าที่อะไร

## Day 2: Windows Identity & Access Control

### ได้เรียนรู้อะไร

Day 2 เป็นเรื่อง identity และ access control บน Windows/Active Directory ผมได้เรียนว่าการจัดการ user ไม่ใช่แค่สร้าง account แต่ต้องคิดเรื่อง OU, group, permission, policy และ password rule ด้วย

ใน Lab 15.1.8 ผมได้สร้าง user account ใน Active Directory โดยต้องใส่ first name, last name, logon name ตามมาตรฐาน `first initial + lastname` เช่น Susan Smith เป็น `ssmith` และต้องเลือก domain `@CorpNet.local`

ผมยังได้เรียนเรื่อง temporary employee เช่น Borey Chan ที่ต้องจำกัด logon hours เฉพาะวันจันทร์ถึงศุกร์ เวลา 8:00 AM-5:00 PM และตั้ง account expiration ให้หมดอายุวันที่ 31 ธันวาคมของปีปัจจุบันใน Lab

ใน Lab 15.2.6 ผมได้เรียนเรื่อง Group Policy Management โดยสร้าง GPO ชื่อ `Temp Workstation Settings`, link ไปที่ OU ของ temporary employees และ import security template `C:\Templates\ws_sec.inf`

ใน Lab 15.3.6 ผมได้ตั้งค่า NTFS permissions ให้โฟลเดอร์ `D:\Day Data` และ `D:\Night Data` โดยต้อง disable inheritance, convert permission เป็น explicit, ลบ group `Users` แล้วเพิ่ม `DayGroup` หรือ `NightGroup` พร้อมให้ Full Control

ใน Lab 19.1.2 ผมได้ตั้ง Local Security Policy เช่น password history, password length, complexity, maximum/minimum password age และ account lockout policy

### ปัญหาที่เจอ

ปัญหาหลักคือ Active Directory มี OU หลายชั้น ทำให้ตอนสร้าง user ต้องระวังมากว่ากำลังสร้างใน OU ถูกต้องหรือไม่ เช่น Marketing Managers, PermSales, SalesManagers และ TempSales

อีกปัญหาคือเรื่อง NTFS permission ตอนแรกผมยังไม่เข้าใจว่าทำไมต้องกด `Disable inheritance` ก่อน ถึงจะลบ group `Users` ออกจาก ACL ได้

ส่วน Lab password policy มีจุดที่ต้องระวังคือเมื่อกำหนด account lockout threshold แล้ว Windows อาจมีหน้าต่าง suggested value เด้งขึ้นมา ทำให้ค่าบางอย่างเปลี่ยนจากที่โจทย์ต้องการ

### แก้ปัญหายังไง

ผมแก้เรื่อง OU โดยอ่านโจทย์เป็นตารางก่อน แล้วจด mapping ว่า user แต่ละคนต้องอยู่ OU ไหน จากนั้นค่อยสร้างทีละคน ไม่รีบกด finish

เรื่อง NTFS inheritance ผมทำความเข้าใจว่า permission ที่ inherited มาจาก parent folder ไม่สามารถลบได้ตรง ๆ จึงต้อง disable inheritance และ convert เป็น explicit permission ก่อน ถึงจะลบ `Users` ออกจาก ACL ได้

สำหรับ password policy ผมตั้งค่าทีละตัว แล้วกลับมาตรวจหน้ารวมอีกครั้งหลังแก้เสร็จ โดยเฉพาะ `Account lockout duration`, `Account lockout threshold` และ `Reset account lockout counter after`

### ได้อะไรจากการแก้ปัญหา

Day 2 ทำให้ผมเข้าใจว่า security ไม่ได้อยู่แค่ antivirus หรือ firewall แต่เริ่มตั้งแต่การจัดการตัวตนและสิทธิ์ของผู้ใช้

ผมได้เห็นหลัก least privilege ชัดขึ้น เช่น ผู้ใช้ควรได้สิทธิ์เท่าที่จำเป็น, temporary employee ควรถูกจำกัดเวลาและวันหมดอายุ, และ folder permission ควรผูกกับ group ที่ถูกต้อง ไม่ใช่เปิดให้ `Users` ทุกคนเข้าถึง

สิ่งที่ได้จากวันนี้คือการคิดแบบ admin มากขึ้น ต้องถามตัวเองว่า:

```text
ใครควรเข้าถึงอะไร
เข้าถึงได้เมื่อไหร่
เข้าถึงได้ระดับไหน
และนโยบายนี้ควรถูกบังคับใช้กับใคร
```

## Day 3: Endpoint Defense & Malware Response

### ได้เรียนรู้อะไร

Day 3 เป็นเรื่อง endpoint defense, malware response และ social engineering ผมได้เรียนว่าความปลอดภัยไม่ได้มีแค่เครื่องมือ แต่ต้องใช้การสังเกตและการตัดสินใจด้วย

ใน Lab 18.1.3 ผมได้แยก email ที่ปลอดภัยออกจาก email อันตราย เช่น phishing, spear phishing, whaling, hoax และ malicious attachment จุดที่สำคัญคือการ hover link เพื่อดู URL จริง และดูว่า email มี digital signature หรือไม่

ใน Lab 19.2.7 ผมได้ใช้ Windows Security/Microsoft Defender Antivirus โดยเพิ่ม file exclusion สำหรับ `D:\Graphics\cat.jpg`, เพิ่ม process exclusion สำหรับ `welcome.scr`, update protection definitions และ run quick scan

ใน Lab 19.2.14 ผมได้วิเคราะห์ workstation security settings เช่น malware detection, quarantine, antivirus component, screen lock, UAC, BitLocker, firewall profile และ firewall exception

ใน Lab 19.5 ผมได้ทำงานแบบ security support ผ่าน ticket จริงมากขึ้น เช่น disable account ที่เสี่ยง, export Security log, เพิ่ม user เข้า security group, ใช้ password generator, ตั้ง BitLocker และ update ticket ให้ถูกสถานะ

### ปัญหาที่เจอ

ปัญหาแรกคือการแยก email อันตรายออกจาก email ปลอดภัย บาง email ดูเหมือนมาจากคนรู้จักหรือหน่วยงานจริง แต่ link หรือ attachment ข้างในมีความเสี่ยง

อีกปัญหาคือใน Applied/Challenge Lab ขั้นตอนค่อนข้างละเอียด และถ้าทำผิด flow แม้แก้บางอย่างถูกก็ยังไม่ได้คะแนน เช่น ticket ของ Angel ต้อง escalate ไม่ใช่ resolved, Frankie ต้องเข้า group `sec-glo-hr`, และ BitLocker ต้องเลือก `Encrypt entire drive` กับ `New encryption mode`

ใน Lab 19.2.14 ผมยังเจอจุดที่ต้องตีความ เช่น firewall exception ที่ไม่ใช่มาตรฐานคือ `Mc` เพราะเป็นรายการที่ถูกเพิ่มเข้ามาเอง ไม่ใช่ exception พื้นฐานที่ Windows ควรอนุญาตไว้ตามปกติ

### แก้ปัญหายังไง

ผมแก้เรื่อง email โดยอ่านเนื้อหาให้ละเอียด ดู sender, ดูคำที่เร่งให้กด link, ดู attachment และ hover link เพื่อเช็ก URL จริง ถ้า link ไม่ตรงกับองค์กรจริง หรือเป็นไฟล์น่าสงสัยก็จัดเป็นอันตราย

สำหรับ Challenge Lab ผมใช้รูป flow ที่ทำได้ถูกต้องมาไล่เทียบทีละขั้น เพื่อดูว่าก่อนหน้านี้พลาดตรงไหน แล้วจึงเขียน README ใหม่ให้ละเอียดขึ้น เช่น Angel ต้องใส่ข้อความ `Done now escalating`, Frankie ต้องใช้ password generator จาก `updates.ad.structureality.com`, และ BitLocker ต้อง save recovery key ไปที่ `C:\SETUP`

ผมยังเริ่มใช้วิธีจดหลักฐานเป็นรูปภาพประกอบขั้นตอน ทำให้ย้อนกลับมาดูได้ว่าตอนนั้นกดอะไร ตั้งค่าอะไร และผลลัพธ์ถูกต้องหรือไม่

### ได้อะไรจากการแก้ปัญหา

Day 3 ทำให้ผมเข้าใจว่า endpoint security ต้องใช้ทั้ง tool และ judgment ถ้ามีแค่เครื่องมือแต่ไม่รู้ว่าควรสังเกตอะไร ก็อาจพลาด phishing หรือ social engineering ได้

ผมได้เรียนว่าการทำ incident response ต้องมีหลักฐาน เช่น log file, screenshot, ticket comment และสถานะ ticket ที่ถูกต้อง เพราะงาน security ไม่ได้จบแค่แก้เครื่อง แต่ต้องมี record ให้คนอื่นตรวจสอบต่อได้

สิ่งที่ได้มากที่สุดคือความเข้าใจว่า security ticket แต่ละใบต้องปิดงานตามประเภทของมัน บางงานปิดได้เอง บางงานต้อง escalate และบางงานต้องเก็บ evidence ก่อนส่งต่อ

## Day 4: Remote Access, Monitoring & Linux

### ได้เรียนรู้อะไร

Day 4 เป็นเนื้อหาที่เชื่อม Windows support เข้ากับ remote access, monitoring และ Linux ผมยังไม่ได้เขียน README แยกแบบละเอียด แต่จากหัวข้อของค่าย วันนี้เน้นการใช้งานเครื่องมือเพื่อเชื่อมต่อและตรวจสอบระบบ

สิ่งที่ได้เรียนในภาพรวมคือการ configure VPN connection, การ monitor process/application, การใช้ informational and network tools และการ configure Linux เบื้องต้น

หัวข้อเหล่านี้ช่วยให้ผมเห็นว่างาน IT ไม่ได้อยู่แค่หน้า GUI ของ Windows แต่ต้องรู้จัก command-line, process, service, network tools และพื้นฐาน Linux ด้วย

### ปัญหาที่เจอ

ปัญหาที่คาดว่าเจอใน Day 4 คือคำสั่งและหน้าตาเครื่องมือมีความหลากหลายมากขึ้น โดยเฉพาะ Linux ที่ syntax ต่างจาก Windows เช่น path, permission, command และการดู network configuration

อีกจุดหนึ่งคือการ monitor process ต้องแยกให้ออกว่า process ไหนเป็นปกติ process ไหนผิดปกติ และควรปิดหรือ investigate ต่อ ไม่ใช่เห็น process แปลกแล้ว kill ทันที

### แก้ปัญหายังไง

วิธีที่ผมใช้คือจดคำสั่งและหน้าที่ของเครื่องมือเป็นกลุ่ม เช่นเครื่องมือสำหรับดู network, เครื่องมือสำหรับดู process, เครื่องมือสำหรับดู service และเครื่องมือสำหรับตรวจ connectivity

ผมพยายามเทียบ Windows กับ Linux ไปพร้อมกัน เช่น Windows ใช้ Task Manager/PowerShell ส่วน Linux ใช้ command-line มากกว่า การเปรียบเทียบแบบนี้ช่วยให้จำ concept ได้ ไม่ได้จำแค่ชื่อเครื่องมือ

### ได้อะไรจากการแก้ปัญหา

Day 4 ทำให้ผมเห็นว่าการ monitor และ remote access เป็นทักษะที่สำคัญมาก เพราะหลายครั้งเราไม่ได้อยู่หน้าเครื่องจริง แต่ต้องเข้าไปตรวจจากระยะไกล และต้องเข้าใจว่าเครื่องกำลังทำอะไรอยู่

สิ่งที่ได้คือแนวคิดว่า ก่อนแก้ปัญหา ต้อง observe ก่อน:

```text
ดูสถานะ -> ดู process/service -> ดู network -> ค่อยตัดสินใจแก้
```

## Day 5: Scripting, IR & Documentation

### ได้เรียนรู้อะไร

Day 5 เป็นเรื่อง scripting, incident response และ documentation แม้ผมยังไม่ได้ทำ write-up แยกเต็ม ๆ แต่หัวข้อนี้สำคัญมาก เพราะเป็นการต่อยอดจากการกดทำทีละขั้น ไปสู่การทำงานแบบอัตโนมัติและมีเอกสารรองรับ

สิ่งที่เรียนคือการ implement PowerShell script, implement Bash script, resolve incident response tickets และการ create/close ticket

PowerShell ช่วยให้งานบน Windows ทำซ้ำได้ง่ายขึ้น ส่วน Bash ช่วยให้ทำงานบน Linux หรือ command-line environment ได้คล่องขึ้น

### ปัญหาที่เจอ

ปัญหาหลักของ scripting คือ syntax ผิดง่ายมาก เช่น path ผิด, quote ผิด, ลืม parameter หรือ output ไม่เป็นแบบที่ต้องการ

อีกปัญหาคือเวลาแก้ incident response ticket ต้องคิดให้ครบทั้ง technical action และ documentation action เพราะถ้าแก้ระบบแล้วไม่ update ticket หรือไม่เขียน comment ให้ชัด งานก็ยังไม่สมบูรณ์

### แก้ปัญหายังไง

ผมใช้วิธีทำ script ทีละส่วน ไม่เขียนยาวทีเดียวแล้วค่อยรัน เพราะถ้าผิดจะหา bug ยาก เริ่มจากคำสั่งเล็ก ๆ ให้ได้ผลก่อน แล้วค่อยรวมเป็น script

สำหรับ ticket ผมใช้แนวคิดว่า comment ต้องตอบให้ได้ว่า:

```text
ทำอะไรไปแล้ว
ทำกับเครื่องหรือ user ไหน
ผลลัพธ์เป็นยังไง
ต้องส่งต่อใครหรือไม่
```

### ได้อะไรจากการแก้ปัญหา

Day 5 ทำให้ผมเห็นว่า documentation เป็นส่วนหนึ่งของงาน technical ไม่ใช่งานเสริม การแก้ปัญหาที่ดีต้องทำให้คนอื่นอ่านต่อแล้วเข้าใจได้

ผมยังได้เรียนว่า scripting ช่วยลดความผิดพลาดจากการทำซ้ำ และทำให้เราทำงานได้เป็นระบบมากขึ้น โดยเฉพาะงานที่ต้องตรวจหลายเครื่องหรือทำขั้นตอนเดิมซ้ำหลายครั้ง

## สรุป Week 1

หลังจบ Week 1 ผมรู้สึกว่าตัวเองเข้าใจภาพรวมของงาน IT support และ security ฝั่ง Windows มากขึ้น จากตอนแรกที่ทำ Lab แบบดูขั้นตอนเป็นหลัก ตอนนี้เริ่มเข้าใจเหตุผลเบื้องหลังมากขึ้น เช่น ทำไมต้องตั้ง gateway, ทำไมต้อง disable inheritance, ทำไมต้องใช้ security group, ทำไมต้องเก็บ recovery key, ทำไมบาง ticket ต้อง escalate

ปัญหาที่เจอส่วนใหญ่ไม่ได้เกิดจากทำไม่ได้เลย แต่เกิดจากยังไม่เข้าใจ context ว่าทำไมต้องทำแบบนั้น พอเริ่มจด write-up พร้อมเหตุผลและรูปประกอบ ผมเลยย้อนกลับมาเข้าใจสิ่งที่ทำมากขึ้น

สิ่งที่ได้จาก Week นี้คือ:

1. เข้าใจพื้นฐาน network และการ troubleshoot เป็นลำดับ
2. เข้าใจการจัดการ user, group, OU, GPO และ permission
3. เข้าใจ password policy และ account lockout policy
4. เข้าใจ endpoint security, Defender, firewall และ social engineering
5. เข้าใจการทำงานผ่าน ticket และการเก็บหลักฐาน
6. เริ่มเห็นความสำคัญของ scripting และ documentation

โดยรวม Week 1 ทำให้ผมมองงาน IT/security เป็นกระบวนการมากขึ้น ไม่ใช่แค่การกดตาม Lab แต่เป็นการอ่านโจทย์ วิเคราะห์ปัญหา ลงมือแก้ ตรวจผล และจดหลักฐานให้คนอื่นเข้าใจต่อได้

## สิ่งที่อยากพัฒนาต่อ

สิ่งที่ผมอยากพัฒนาต่อคือการจำคำสั่งและเครื่องมือให้คล่องขึ้น โดยเฉพาะฝั่ง Linux, PowerShell และ Bash เพราะถ้าใช้ command-line ได้ดี จะช่วย troubleshoot และ automate งานได้เร็วขึ้น

อีกอย่างที่อยากฝึกคือการเขียน incident/ticket comment ให้กระชับแต่ครบถ้วน เพราะในงานจริง comment ที่ดีช่วยให้ทีมอื่นรับช่วงต่อได้ง่าย และลดการถามซ้ำ

สำหรับ Week ถัดไปอย่าง TryHackMe และ Root the Box ผมอยากเอาพื้นฐานจาก CompTIA A+ ไปต่อยอดกับการคิดแบบ attacker/defender ให้มากขึ้น เพื่อให้เข้าใจ security ทั้งฝั่งป้องกันและฝั่งโจมตี
