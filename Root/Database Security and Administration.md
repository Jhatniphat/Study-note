Database Security includes
- Hardware
- Software
- People
- Data or Database
มีเป้าหมายเพื่อป้องกันสถานการณ์ดังนี้
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
