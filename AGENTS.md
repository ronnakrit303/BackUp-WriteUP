# AGENTS.md

## ภาพรวมโปรเจกต์

โปรเจกต์นี้เป็นพื้นที่สำหรับเก็บและจัดทำ write-up ของงาน CompTIA A+ Core 1 and Core 2 CertMaster Perform โดยแยก Lab แต่ละหัวข้อเป็นโฟลเดอร์ของตัวเอง ภายในแต่ละ Lab จะมี `README.md` สำหรับอธิบายขั้นตอนการทำ และมีโฟลเดอร์ `images/` สำหรับเก็บรูปภาพประกอบ

มาตรฐานปัจจุบันของโปรเจกต์คือ README ของแต่ละ Lab ควรเขียนเป็นภาษาไทยแบบอ่านตามได้จริง มีเหตุผลประกอบว่าทำไมต้องทำแต่ละขั้นตอน และวางรูปภาพไว้ใต้ขั้นตอนที่เกี่ยวข้องโดยตรง ไม่แยกรูปไปไว้ท้ายไฟล์เป็นหัวข้อหลักฐาน

## โครงสร้างโปรเจกต์ปัจจุบัน

```text
CompTIA A+/
+-- 6.2.7 Lab Configure IP Addresses/
|   +-- README.md
|   +-- images/
+-- 7.3.3 Lab Fix a Network Connection/
|   +-- README.md
|   +-- images/
+-- 7.4 Lab Troubleshoot a Network Issue/
|   +-- README.md
|   +-- images/
+-- 13.3.9 Lab Local Firewall Settings/
|   +-- README.md
|   +-- images/
+-- 15.1.8 Lab Create User Accounts/
|   +-- README.md
|   +-- images/
+-- 15.2.6 Lab Group Policy Management/
|   +-- README.md
|   +-- images/
+-- 15.3.6 Lab Configure NTFS Permissions/
|   +-- README.md
|   +-- images/
+-- 19.1.2 Lab Enforce Password Settings/
    +-- README.md
    +-- images/
```

## งานที่ทำไปแล้ว

### 1. Lab 6.2.7: Configure IP Addresses

Lab นี้เป็นการตั้งค่า IPv4 แบบ static ให้กับเครื่อง `Exec` ที่มี network adapter 2 ตัว คือ `Ethernet` และ `Ethernet 2`

ค่าหลักที่ใช้ใน Lab:

```text
Ethernet
IP address: 192.168.0.254
Subnet mask: 255.255.255.0
Default gateway: 192.168.0.5
Preferred DNS: 163.128.78.93
Alternate DNS: 163.128.80.93

Ethernet 2
IP address: 10.0.255.254
Subnet mask: 255.255.0.0
Default gateway: Blank
DNS: Blank
```

README อธิบายเรื่อง subnet, วิธีหา last valid address, เหตุผลที่ต้องใส่ gateway เฉพาะ `Ethernet` และการทดสอบด้วย `ping`

ผลลัพธ์:

```text
Score: 100%
```

รูปที่ใช้ใน README:

```text
01-network-exhibit.png
02-ethernet-ipv4-config.png
03-ethernet2-ipv4-config.png
04-ping-preferred-dns.png
05-score-100.png
```

### 2. Lab 7.3.3: Fix a Network Connection

Lab นี้เป็นการ troubleshoot เครื่อง `Office1` ที่ไม่สามารถใช้งาน network และ internet ได้ โดยพบทั้งปัญหา hardware และ software configuration

ปัญหาที่พบ:

```text
สาย LAN ไม่ได้เชื่อมต่อถูกต้อง
เครื่องใช้ Automatic DHCP ทั้งที่ network ไม่มี DHCP server
เครื่องได้ APIPA address ขึ้นต้นด้วย 169.254.x.x
DNS เดิมไม่ถูกต้อง
```

ค่าที่ใช้แก้ไข:

```text
IP address: 192.168.0.35
Subnet mask: 255.255.255.0
Default gateway: 192.168.0.5
Preferred DNS: 163.128.78.93
Alternate DNS: 163.128.80.93
```

ผลลัพธ์:

```text
Score: 100%
Ping Office2 สำเร็จ
Ping DNS server สำเร็จ
```

รูปที่ใช้ใน README:

```text
01-network-exhibit.png
02-ipconfig-media-disconnected.png
03-hardware-cable-connected.png
04-ethernet-before-apipa-dhcp.png
05-manual-ipv4-settings.png
06-ethernet-after-static-config.png
07-ipconfig-and-ping-success.png
08-score-100.png
```

### 3. Lab 7.4: Troubleshoot a Network Issue

Lab นี้เป็นการแก้ ticket ในระบบ `Issue Trax` โดย ticket แจ้งว่า laptop ใน `Office 2` ไม่สามารถเชื่อมต่อ `CorpNet wireless network` ได้

สาเหตุของปัญหา:

```text
Wireless switch บนตัว Office2-Lap อยู่ตำแหน่ง OFF
```

วิธีแก้ไข:

```text
ตรวจสอบ ticket
ทดสอบว่า ITAdmin เชื่อมต่อ CorpNet ได้
ไปที่ Office2-Lap
เปิด wireless switch บนตัวเครื่อง
เชื่อมต่อ CorpNet wireless network
กลับไป comment และปิด ticket
```

ผลลัพธ์:

```text
Score: 100%
Connect the laptop in Office 2 to the CorpNet wireless network: Completed
```

รูปที่ใช้ใน README:

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
10-floor-overview-office2.png
```

### 4. Lab 13.3.9: Local Firewall Settings

Lab นี้เป็นการตั้งค่า Windows Firewall สำหรับ `Public network profile` เท่านั้น เพราะสถานการณ์คือ laptop จะถูกนำไปใช้กับ public Wi-Fi เช่น airport hotspot

สิ่งที่ทำใน Lab:

```text
เปิด Windows Firewall สำหรับ Public network profile
Allow Key Management Service เฉพาะ Public
Allow Cloud Identity เฉพาะ Public
Allow File and Printer Sharing เฉพาะ Public
```

เหตุผลหลักคือเปิดสิทธิ์เฉพาะ profile ที่โจทย์กำหนด เพื่อลดการเปิดสิทธิ์เกินความจำเป็นและลด attack surface

ผลลัพธ์:

```text
Score: 100%
Turn Windows Firewall on: Completed
Allow Key Management Service through the Public firewall: Completed
Allow Cloud Identity through the Public firewall: Completed
Allow File and Printer Sharing through the Public firewall: Completed
```

รูปที่ใช้ใน README:

```text
01-windows-security-overview.png
02-firewall-profiles-public-off.png
03-public-firewall-on.png
04-public-network-allow-app-link.png
05-allowed-apps-before-public-checks.png
06-key-management-service-public.png
07-cloud-identity-public.png
08-file-and-printer-sharing-public.png
09-score-100.png
```

### 5. Lab 15.1.8: Create User Accounts

Lab นี้เป็นการสร้างบัญชีผู้ใช้ใน Active Directory บนเครื่อง `CorpDC` โดยต้องสร้าง user ให้ถูก OU, ตั้ง logon name ตามมาตรฐาน, ตั้งรหัสผ่านเริ่มต้น และเพิ่ม restriction ให้ temporary employee

บัญชีที่สร้าง:

```text
Juan Suarez
OU: Marketing\MarketingManagers
Logon name: jsuarez

Susan Smith
OU: Sales\PermSales
Logon name: ssmith

Mark Burnes
OU: Sales\SalesManagers
Logon name: mburnes

Borey Chan
OU: Sales\TempSales
Logon name: bchan
```

ค่ารหัสผ่านที่ใช้กับทุกบัญชี:

```text
Password: asdf1234$
User must change password at next logon: Enabled
Domain: @CorpNet.local
```

ข้อจำกัดเพิ่มเติมของ `Borey Chan`:

```text
Logon hours: Monday-Friday, 8:00 AM-5:00 PM
Account expires: December 31, 2026
```

ผลลัพธ์:

```text
Score: 100%
Create the Juan Suarez account: Completed
Create the Susan Smith account: Completed
Create the Mark Burnes account: Completed
Create the Borey Chan account: Completed
```

รูปที่ใช้ใน README:

```text
01-hyper-v-corpdc-selected.png
02-server-manager-tools-aduc.png
03-active-directory-ou-overview.png
04-juan-suarez-user-info.png
05-user-password-must-change.png
06-susan-smith-user-info.png
07-susan-smith-password.png
08-mark-burnes-user-info.png
09-mark-burnes-password.png
10-borey-chan-user-info.png
11-borey-chan-password.png
12-borey-logon-hours-weekday-business-hours.png
13-borey-account-expiration.png
14-score-100.png
```

### 6. Lab 15.2.6: Group Policy Management

Lab นี้เป็นการสร้าง Group Policy Object หรือ GPO บนเครื่อง `CorpDC` เพื่อบังคับใช้นโยบายความปลอดภัยกับ workstation ของ temporary employees

สิ่งที่ทำใน Lab:

```text
สร้าง GPO ชื่อ Temp Workstation Settings
Link GPO ไปที่ Marketing\TempMarketing
Link GPO ไปที่ Sales\TempSales
Import security template จาก C:\Templates\ws_sec.inf
```

เหตุผลหลักคือ workstation ของ temporary employees ควรได้รับ security policy ที่เฉพาะเจาะจง โดยใช้ GPO เดียวแล้ว link ไปยัง OU ที่เกี่ยวข้อง ทำให้จัดการ policy ได้ง่ายและสม่ำเสมอ

ผลลัพธ์:

```text
Score: 100%
Create the Temp Workstation Settings GPO: Completed
Link the GPO to the TempMarketing OU: Completed
Link the GPO to the TempSales OU: Completed
Import the policy from C:\Templates\ws_sec.inf: Completed
```

รูปที่ใช้ใน README:

```text
01-server-manager-dashboard.png
02-tools-group-policy-management.png
03-group-policy-domain-overview.png
04-new-gpo-temp-workstation-settings.png
05-gpo-created.png
06-link-tempmarketing-select-gpo.png
07-link-tempsales-select-gpo.png
08-import-policy-from-security-settings.png
09-select-ws-sec-template.png
10-score-100.png
```

### 7. Lab 15.3.6: Configure NTFS Permissions

Lab นี้เป็นการตั้งค่า NTFS permissions ให้กับโฟลเดอร์ `D:\Day Data` และ `D:\Night Data` บนเครื่อง `Office1`

สิ่งที่ทำใน Lab:

```text
ปิด permissions inheritance
Convert inherited permissions เป็น explicit permissions
ลบ Users ออกจาก ACL
เพิ่ม DayGroup ให้ D:\Day Data
เพิ่ม NightGroup ให้ D:\Night Data
ให้กลุ่มที่ถูกต้องเป็น Full Control
ไม่เปลี่ยน permission อื่นที่ไม่เกี่ยวข้อง
```

ค่าหลักที่ใช้:

```text
D:\Day Data
Group: DayGroup
Permission: Full Control

D:\Night Data
Group: NightGroup
Permission: Full Control
```

ผลลัพธ์:

```text
Score: 100%
Edit permissions for the D:\Day Data folder: Completed
Edit permissions for the D:\Night Data folder: Completed
```

รูปที่ใช้ใน README:

```text
01-data-drive-folders.png
02-day-data-security-tab.png
03-day-data-convert-inheritance.png
04-day-data-remove-users.png
05-add-daygroup.png
06-daygroup-full-control.png
07-night-data-security-tab.png
08-night-data-convert-inheritance.png
09-night-data-remove-users.png
10-add-nightgroup.png
11-nightgroup-full-control.png
12-score-100.png
```

### 8. Lab 19.1.2: Enforce Password Settings

Lab นี้เป็นการตั้งค่า `Local Security Policy` บนเครื่อง `Gst-Lap` ใน Lobby เพื่อบังคับกฎรหัสผ่านและ account lockout policy

ค่าที่ตั้งใน Password Policy:

```text
Enforce password history: 4
Maximum password age: 30
Minimum password age: 2
Minimum password length: 10
Passwords must meet complexity requirements: Enabled
```

ค่าที่ตั้งใน Account Lockout Policy:

```text
Account lockout duration: 60
Account lockout threshold: 4
Reset account lockout counter after: 40
```

จุดสำคัญของ Lab นี้คือหลังตั้ง `Account lockout threshold` อาจมีกล่อง `Suggested Value Changes` เด้งขึ้นมา ต้องกด `OK` แล้วกลับไปแก้ค่า `Account lockout duration` และ `Reset account lockout counter after` ให้ตรงกับโจทย์

ผลลัพธ์:

```text
Score: 100%
Remember the last four passwords: Completed
Force password changes every 30 days: Completed
Do not allow password changes within two days: Completed
Require passwords of ten characters or more: Completed
Require complex passwords: Completed
Lock accounts after four invalid attempts: Completed
Unlock locked accounts after 60 minutes: Completed
Reset the account lockout counter after 40 minutes: Completed
```

รูปที่ใช้ใน README:

```text
01-windows-tools-local-security-policy.png
02-password-policy-before.png
03-enforce-password-history-4.png
04-maximum-password-age-30.png
05-minimum-password-age-2.png
06-minimum-password-length-10.png
07-password-complexity-enabled.png
08-password-policy-configured.png
09-account-lockout-threshold-4.png
10-suggested-value-changes.png
11-account-lockout-duration-60.png
12-reset-lockout-counter-40.png
13-account-lockout-policy-configured.png
14-score-100.png
```

## มาตรฐานการจัดรูปภาพ

รูปภาพที่ใช้จริงใน README ควรตั้งชื่อแบบมีเลขนำหน้า เช่น:

```text
01-...
02-...
03-...
```

ถ้ามีหลายรูปที่สื่อความหมายเดียวกัน ให้เลือกรูปที่อ่านง่ายที่สุดและเหมาะกับขั้นตอนมากที่สุด ส่วนรูปที่ไม่ได้ใช้ให้เปลี่ยนชื่อเป็น `unused-...` เพื่อเก็บไว้โดยไม่ทำให้สับสนกับรูปที่ใช้จริง

รูปภาพใน README ควรอยู่ใต้ขั้นตอนที่เกี่ยวข้องโดยตรง เช่น รูปตั้งค่า password ควรอยู่ใต้ขั้นตอนตั้งค่า password ไม่ควรถูกย้ายไปอยู่รวมท้ายไฟล์

## สถานะปัจจุบัน

Lab ที่ทำ README และจัดรูปภาพเสร็จแล้ว:

```text
6.2.7 Lab Configure IP Addresses: 100%
7.3.3 Lab Fix a Network Connection: 100%
7.4 Lab Troubleshoot a Network Issue: 100%
13.3.9 Lab Local Firewall Settings: 100%
15.1.8 Lab Create User Accounts: 100%
15.2.6 Lab Group Policy Management: 100%
15.3.6 Lab Configure NTFS Permissions: 100%
19.1.2 Lab Enforce Password Settings: 100%
```

## แนวทางสำหรับ Lab ถัดไป

ถ้ามี Lab ใหม่ ให้สร้างโครงสร้างแบบเดิม:

```text
CompTIA A+/
+-- <Lab Name>/
    +-- README.md
    +-- images/
```

README ของแต่ละ Lab ควรมี:

1. ชื่อ Lab
2. ภาพรวมของ Lab
3. วัตถุประสงค์
4. สิ่งที่ต้องตั้งค่าหรือข้อมูลที่ต้องใช้
5. วิธีคิดหรือวิธีคำนวณ ถ้า Lab นั้นมี
6. ขั้นตอนการทำแบบละเอียด
7. เหตุผลว่าทำไมต้องทำแต่ละขั้นตอน
8. รูปภาพประกอบทุกขั้นตอนสำคัญ โดยวางไว้ใต้ขั้นตอนนั้นโดยตรง
9. สรุปผลลัพธ์สุดท้ายและคะแนน Lab
