#### Summary
Computer-based Security Controls
- Authorization
- Access controls
- Views
- Backup and recovery
- Integrity
- Encryption
- RAID technology
Database Security includes
- Hardware
- Software
- People
- Data or Database
มีเป้าหมายเพื่อป้องกันสถานการณ์ดังนี้ ( minimize loss)
- heft and fraud ( การโจรกรรมข้อมูล )
- Loss of confidentiality (maintain secrecy)  -- การรักษาความลับไม่ได้
- Loss of privacy (protect individual data) -- รักษาความเป็นส่วนตัวของบุคคลไม่ได้
- Loss of integrity (invalid or corrupted data) -- ข้อมูลผิดพลาด 
- Loss of availability (access data or system) -- เข้าถึงข้อมูลไม่ได้
Security plan of Organization
- การ Organization จะต้อง
	- identify all possible threats -- วิเคราะห์ภัยคุมคามที่เป็นไปได้
- Model
	- ![Pasted image 20240207101835.png](./Pasted%20image%2020240207101835.png)
	- Authentication - คุณเป็นใคร
	- Authorization - ใครมีสิทธิ? ในการเข้าถึง
	- Encryption - การเข้ารหัสข้อมูล
	- Audit - การตรวจสอบประวัติที่ผ่านมา
		- เราไม่ Audit ทุกคนทุกอย่าง เพราะมันจะทำให้ DB ช้า
		- เราจะ Audit เฉพาะสิ่งที่สำคัญและมีผลต่อธุรกิจของเรา
Access Controls
- Privilege
	- คล้าย ๆ กับ Permission แต่เป็นในเชิง DB
	- จะทำอะไรก็ตามในฐานข้อมูลจะต้องมี Privilege
	- ปกติจะจัดการผ่าน **Discretionary Access Control (DAC)**
		- นอกเหนือจาก DBA หรือ Admin ผู้ที่เป็น Owner ของ Object นั้น ๆ จะมีสิทธิแก้ไขได้เสมอ
		- ให้สิทธิเต็มที่กับคนที่เป็น Owner
		- ถ้าเราเป็นคนสร้างตาราง เราสามารถบริหารจัดการตารางของตัวเองได้ ไม่จำเป็นต้องรอแอดมินเท่านั้น
		- มีช่องโหว่ที่ owner อาจจะให้สิทธิใครบางคนมากเกินไป
	- เพื่อแก้ช่องโหว่ของ DAC จึงเกิด **Mandatory Access Control (MAC)**
		- การจะบริหารสิทธิจะผ่านส่วนกลาง หรืออ้างอิง Policy กลางที่ตั้งเอาไว้
		- สมมุติว่าไปซื้อปากกา ปากกาจะเป็นขององค์กร จะให้ใครได้ หรือให้ใครไม่ได้
		- มีข้อเสียคือ มีความยืดหยุ่นน้อย
- Database Administrator (DBA)
	- จะใช้ Superuser account (ใน mySql คือ root)
- Data Administrator (DA)
	- คนละคนกับ DBA นะ
	- มีหน้าที่บริหารการจัดการข้อมูลภายในองค์กร

##### การสร้าง User
```
CREATE USER <username> IDENTIFIED BY <password> PASSWORD EXPIRE ACCOUNT LOCK| ACCOUNT UNLOCK];
```
- Password Expire คือให้ password หมดอายุตอนเข้าใช้ครั้งแรก
- username ใน mysql จำเป็นจะต้องกำหนด Host ด้วย ถ้าไม่ระบุจะเก็บเป็น % แสดงว่ามาจากเครื่องไหนก็ได้
- ```CREATE USER 'jeffrey'@'localhost' IDENTIFIED BY 'password';```
- ตอนสร้างกำหนด password เป็น plain text แต่ระบบจะเก็บเป็นแบบเข้ารหัส
- ข้อมูลของ User จะถูกเก็บได้ `mysql.user`
- สามารถกำหนดจำนวนการล็อกอินเพื่อป้องกันการแฮค
	```
	FAILED_LOGIN_ATTEMPTS 3 // จำนวนครั้งที่กรอกผิดได้
	PASSWORD_LOCK_TIME 2 // ให้ล็อค user กี่วัน ;
	```
- 
#### Privileges
##### การให้สิทธิ User
###### Global Privileges
```
GRANT ALL ON *.* TO 'someuser'@'somehost';
GRANT SELECT, INSERT ON *.* TO ‘someuser'@'somehost';
```
เป็นการให้สิทธิทุก DB ทุกตาราง ให้กับ user
###### Database Privileges
```
GRANT ALL ON mydb.* TO 'someuser'@'somehost';
GRANT SELECT, INSERT ON mydb.* TO ‘someuser'@'somehost';
```
เป็นการให้สิทธิทุกตารางใน DB นั้น ๆ
ดูการให้สิทธิได้ใน `mysql.DB`
###### Table Privileges
```
GRANT ALL ON mydb.mytbl TO 'someuser'@'somehost';
GRANT SELECT, INSERT ON mydb.mytbl TO ‘someuser'@'somehost';
```
เป็นการให้สิทธิในตารางนั้น ๆ
ดูการให้สิทธิได้ใน `mysql.tables_priv`
###### Column Privileges
```
GRANT SELECT (col1), INSERT (col1, col2) ON mydb.mytbl TO ‘someuser'@'somehost';
```
ให้เฉพาะเจาะจงกับบาง column
ดูการให้สิทธิได้ใน `mysql.columns_priv`

##### การขอสิทธิคืนจาก User
ใช้คำสั่ง Revoke
```
REVOKE select, update ON classicmodels.customers FROM ‘jeffrey'@'localhost';
```
##### การเช็คสิทธิของ User
ใช้คำสั่ง Show grant
```
SHOW GRANTS FOR 'jeffrey'@'localhost';
```
ถ้าไม่ใส่ For จะเป็นการเช็คสิทธิของตัวเอง
ถ้ามีสิทธิเป็น USAGE คือแค่ล็อกอินได้

#### Backup and Recovery
###### ในหัวข้อนี้จะพูดถึงการ minimize loss อยู่ 2 ข้อ
- Loss of integrity (invalid or corrupted data) 
- Loss of availability (access data or system)
##### Integrity
หากควบคุมเรื่องเหล่านี้ได้ จะสามารถควบคุม Loss of integrity
###### Integrity constraints
- Integrity -> ความซื่อสัตย์
- Constraints -> ข้อกำหนดต่าง ๆ
- กฎข้อบังคับต่างๆ ที่ทำให้เกิดความถูกต้องสมบูรณ์ (ของข้อมูล)
- มีส่วนร่วมในการดูแลรักษาระบบฐานข้อมูลให้มีความปลอดภัยโดยไม่ให้ข้อมูลเกิดความผิดพลาด
###### Type of integrity constraints
- Required Data
- Domain constraints
- Multiplicity
- Entity integrity
- Referential integrity
- General constraints
##### Errors and Failures
###### Human Errors
- อาจจะเกิดจากความไม่เข้าใจในตัวโปรแกรม
- อาจจะเผลอลบข้อมูลใน DB
- เป็นสาเหตุใหญ่ ๆ ของ Data loss
###### Media Failures/Disk Failure
- เกิดจาก Disk ได้รับความเสียหาย อาจจะเกิดได้ทั้งจากทางกายภาพและ Logic
##### Backup and Recovery

###### Backup 
- คอย copy ฐานข้อมูลเป็นระยะ ๆ 
- อาจจะต้องคุยกันว่าจะ Backup ทุก ๆ เวลาเท่าไหร่
###### Journaling
- ใช้ไฟล์ในการเก็บประวัติการเปลี่ยนแปลงด้วย
- เช่น log ไฟล์
###### Backup and Recovery Types
- **Physical Backup ( Raw )**
	- copy ไฟล์ ที่เป็น raw data เลย <- copy ไฟล์จาก Directory ในเครื่องเลย
	- เหมาะกับ DB ขนาดใหญ่ ๆ เพราะมีความเร็วกว่า Logical Backup
	- มีความเร็วในการ Backup มากกว่าเพราะไม่จำเป็นต้อง convert อะไร
	- ขึ้นอยู่กับ Storage engine ที่เลือกใช้ด้วย ถ้า innoDB จะไม่ค่อยมีปัญหา แต่ถ้าเป็น MyIsam ก็อาจจะกำหนดอะไรได้ไม่เยอะ
	- ข้อมูลที่ย้ายไปลงในอีกเครื่องหนึ่ง จำเป็นจะต้องมี config ที่เหมือนกันทุกประการ
	- มีเครื่องมือ mySQL Backup ให้เลือกใช้ ( mysql enterprise นะจ๊ะ )
- **Logical Backup**
	- Backup อยู่ในรูปแบบของ Script
	- เช่น ถ้า classicmodels มีปัญหา ก็นำ Script มา Run ใหม่
	- มีความคล่องตัวสูงกว่า แต่เหมาะกับข้อมูลเล็ก ๆ
	- มีความยืดหยุ่นกว่า จะย้ายไป run ในอีกเครื่องก็ได้ ขอแค่สามารถรัน mysql ได้
	- เราจะใช้ ==mysqldump== เป็น tool ในการทำ ( เป็น CLI )
	- ตอน restore กลับก็แค่นำ Script มา Run
	- หากไม่ได้ใช้ .mysql แต่เป็นไฟล์แบบอื่น เช่น .csv สามารถใช้ ==mysql import==
###### Online vs Offline Backups
- Online Backups
	- User ยังคงจะเข้ามาอ่านข้อมูลได้
	- เป็นการ Backups ที่ไม่กระทบกับ User
	- มีการ Locking ไม่ให้ User สามารถแก้ไขข้อมูลได้
- Office Backups
	- เป็นการ Shutdown DB แล้วค่อย Backups
	- การันตีได้ว่าจะไม่มีใครมายุ่งกับข้อมูลขณะ Backups อยู่
	- ควรทำใน DB ที่ไม่มี impact ต่อธุรกิจมากนัก
###### Full vs Incremental Backup
- Full Backups 
	- Backups ทุกอย่าง
- Incremental Backups 
	- Backups เฉพาะสิ่งที่ถูกเปลี่ยนแปลง
	- จำเป็นต้องมีการ Full Backups ก่อนอย่างน้อย 1 ครั้ง เพื่อเปรียบเทียบความ
###### Full vs Point-in-Time ==Recovery==
- ต้องนำ Full Backups มา Recovery ก่อน
- แล้วนำ Incremental Backups หรือ logfile มา Restore ต่อจากเวลาตอนที่ Backups แบบ Full
##### Concepts
###### Backup Concepts in MySQL
- ขึ้นอยู่กับ User
	- End User : ปกติ ก็อาจจะ Backup ข้อมูลในตารางที่ตนเองอยู่ก่อนจะทำอะไร
	- DBA : Backup ตารางด้วย EXPORT utility.
	- DBA : Backup the database using Recovery Manager with BACKUP command 
###### Recovery Concepts
- ขึ้นอยู่กับ User
	- End User : นำ Script ใหม่
	- End User : ใช้เทคนิคการ Flashback ( ย้อนกลับไปในเวลานั้น ๆ )
	- DBA : Recovery ตารางด้วย IMPORT utility.
	- DBA : Recovery the database point in time using Backup files and Log files
- In case of disk failures
	- DBA : ใช้ Full database backups ในการ Recovery
	- DBA : Recovery the database point in time using Backup files and Log files
- In case System Crash
	- DBMS จะทำการเช็ค log ไฟล์ เช่น REDO-type , UNDO-type แล้วทำการ Recovery ให้โดยอัตโนมัติ
	- DBMS จะกู้คืนทุกอย่างที่ User Save แต่อันไหนที่ไม่มีใน log file หรือ User ไม่ได้ Save ก็จะถูกยกเลิก
##### RAID ( Redundant Array of Independent Disk )
###### concept
- นำ disk มาต่อกันหลาย ๆ ลูก แล้วทำเสมือนเป็น disk ลูกเดียว
- performance  Improvement เพราะ data striping เพราะสามารถอ่านข้อมูลได้หลาย ๆ disk พร้อม ๆ กัน
- Reliability Improvement เพราะข้อมูลจะถูกเก็บข้าม disk แบบเท่าเทียมกัน
###### Raid Level
- RAID 0 Non-redundant 
- RAID 1 Mirrored 
- RAID 2 Memory-Style Error-Correcting Codes 
- RAID 3 Bit-Interleaved Parity 
- RAID 4 Block-Interleaved Parity
- RAID 5 Block-Interleaved Distributed Parity <- ( ได้รับความนิยม )
	- ถ้า Disk พังลูกเดียว สามารถกู้คืนได้
- RAID 0+1 Non-redundant and Mirrored
- ![Pasted image 20240228105643](./Pasted%20image%2020240228105643.png)![Pasted image 20240228105654](./Pasted%20image%2020240228105654.png)![Pasted image 20240228105708](./Pasted%20image%2020240228105708.png)