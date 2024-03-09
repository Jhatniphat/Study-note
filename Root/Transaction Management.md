Transaction Management
### Transaction
##### Definition
- Action, or series of actions, carried out by user or application, whichreads or updates contents of database.
- การกระทำหรือชุดของการกระทำที่ดำเนินการโดยผู้ใช้หรือแอปพลิเคชัน==ซึ่งอ่านหรืออัพเดตเนื้อหาของฐานข้อมูล==
- 1 Transaction อาจจะประกอบไปด้วยหลาย Operation เช่น นาย A อาจจจสั่งให้เขียนแล้วค่อยอ่าน ก็ถือเป็น 1 Transaction
##### State of Transaction
- ![Pasted image 20240306092905.png](./Pasted%20image%2020240306092905.png)
- ==ไม่ตายตัวในแต่ละผลิตภัณฑ์==
- บางผลิตภัณฑ์จะใช้คำอื่นที่ไม่ใช่ Begin Transaction จะใช้ Start Transaction แทน และในบางตัวก็อาจจะไม่มีขั้นตอนนี้ แต่จะถือจัดการด้วย DML แบบอัตโนมัติ
- เมื่อทำงานเสร็จแล้ว ก็จะทำการ COMMITED เพื่อยืนยันการแก้ไขข้อมูล
- หลังจาก COMMITED เสร็จแล้ว ก็จะทำให้ข้อมูลเป็นเวอร์ชันถัดไปทันที
- ACTIVE
	- Executes database and non-database operations
- COMMITED
- ABORTED
- PARTIALL COMMITED
	- Occurs after the final statement has been executed
	- It may be found that transaction has violated an integrity constraint
- FAILED
	- Occurs when transaction cannot be committed or transaction is aborted
	- The user might abort the transaction
	- The concurrency control protocol might abort the transaction to ensure serializability
##### Outcome of Transaction
Commited
- Transaction completes successfully
- The database reaches a new consistent state
ABORTED
- Transaction does not execute successfully
- The database must be restored to the consistent state (previous consistent state) before it started (Rolled back or undone)
Transaction ที่ Commit ไปแล้ว จะไม่สามารถย้อนกลับได้แล้ว
แต่ ถ้าถูก Aborted จะยังสามารถย้อนกลับได้
##### Properties of Transactions (ACID)
มีอยู่ 4 แบบหลัก ๆ
###### Atomicity
- An Indivisible unit
- All or Nothing
###### Consistency
- Database transforms from one consistent state to another consistent state (consistent before and after transaction)
- สมมุติว่า Transaction อัพเดทเงินเดือนเป็น 18,000 จาก 15,000 ถ้ามีคนมาดูระหว่างนี้จะเห็นเป็น 15,000 แต่หลังจาก Commit เสร็จแล้วจะเห็นเป็น 18,000
###### Isolation
- Executes independently of one another (not interfere with each other).
- Transaction จะต้องไม่รบกวนกันเอง สมมุติว่า
###### Durability
- The completed transaction is permanently recorded in database.
- The completed transaction must not be lost from failure.
##### Example
ขั้นตอนการโอนเงิน
```mysql
START TRANSACTION;
SELECT balance FROM checking WHERE customer_id = 10233276;
UPDATE checking SET balance = balance - 200.00 WHERE customer_id = 10233276;
UPDATE savings SET balance = balance + 200.00 WHERE customer_id = 10233276;
COMMIT;
```
หากมีขั้นตอนใดล้มเหลว ก็ต้องทำใหม่ทั้งหมด
### Transaction Subsystem
![Pasted image 20240306095008.png](./Pasted%20image%2020240306095008.png)
#### Concurrency Control
- To maximize concurrency without allowing concurrently executing transactions to interfere with each other
- พยายามจัดการ Transaction ไม่ให้ชนกันหรือเกิดปัญหา
- สมมุติว่า ช่วงที่คนเข้ามาซื้อของ ดูเฉพาะสิ่งที่ตนสนใจ ( ต่างคนต่าง Read )ก็จะไม่มีปัญหา แต่ถ้าหากมีใครบางคนไปอัพเดทข้อมูล จะเกิดปัญหา
- ถ้ามีคนอัพเดทข้อมูลคนเดียว ก็ไม่มีปัญหา แต่ข้อมูลที่ Read ไปก่อนหน้าจะผิดพลาดได้
- ถ้ามีคนอัพเดทข้อมูลเดียวกันหลายคน คนมาหลังจะต้องรอคนก่อนหน้าทำเสร็จก่อน
##### Problems in Concurrency
- ###### Lost update problem
	- มีคนเขียนทับข้อมูลที่เราอัพเดทไป
	- T ใหญ่ แทน Transaction , t เล็ก แทนเวลา![Pasted image 20240306100110.png](./Pasted%20image%2020240306100110.png)จะเห็นได้ว่ามีการเขียน 90 ทับ 200 ไป
- ###### Uncommitted dependency (dirty read)
	- อ่านข้อมูลได้อ่านได้นั้น ไม่ถูกต้อง
	- T ใหญ่ แทน Transaction , t เล็ก แทนเวลา![Pasted image 20240306100530.png](./Pasted%20image%2020240306100530.png)จะเห็นได้ว่ามีการอ่านข้อมูลที่สุดท้ายแล้วมีการ Rollback ( ยังไม่ commit )
- ###### Inconsistent analysis problem
	- T ใหญ่ แทน Transaction , t เล็ก แทนเวลา![Pasted image 20240306100903.png](./Pasted%20image%2020240306100903.png)จะเห็นได้ที่ t4 มีการเอาค่า bal ( 100 ) ไป + sum ทำให้ sum เป็น 100 แต่ T5 มีการลบค่า bal เป็น ( 90 ) ทำให้ค่า sum สุดท้ายนั้นผิดพลาด
###### Inconsistent Retrieval Problems
Interference causes inconsistency among multiple
retrievals of a subset of data
- Incorrect summary (Inconsistent analysis problem)
- Non-repeatable (or fuzzy) read
- Phantom read
##### Serializability and Recoverability
- เวลาที่มีหลาย ๆ transactions ทำงานพร้อมกัน Database อาจจะอยู่ใน Inconsistent state ( transaction ยังไม่เรียบร้อย )
- Serializability เป็น Concept ที่พยายามจัดการ transaction ให้มันรันตามลำดับ หรือให้มันรันเสมือนว่ามันรันตามลำดับเพราะบางอย่างก็ทำแบบ parallel ได้
###### Serial Schedule vs. Non-serial Schedule
- Serial Schedule
	- ทำงานเป็นลำดับขั้นตอน
	- Transaction ที่หนึ่งจบก่อน Transaction ที่สองถึงจะเริ่มทำงานต่อได้
- Non-Serial Schedule
	- บาง Transaction สามารถทำงานพร้อม ๆ กันได้ แต่ยังคงไม่กระทบกัน
	- จะเกิดขึ้นในกรณีที่ยุ่งเกี่ยวกับข้อมูลคนละชุดกัน เพราะยังไงก็ไม่กระทบกัน
###### Serializability 
- บางครั้งก็ไม่ได้รันตามลำดับ แต่ก็ยังคงเสมือนว่ายังรันตามลพดับอยู่
- ใน Serializability , ลำดับการอ่านหรือเขียนเป็นเรื่องสำคัญ
	- ถ้า Transaction ทั้งสอง เป็นอ่านทั้งคู่ ก็จะไม่มีปัญหา ลำดับจึงไม่สำคัญ
	- ถ้า Transaction ทั้งสอง แก้ไขหรืออ่านข้อมูลคนละชุด ก็จะไม่มีปัญหา ลำดับจึงไม่สำคัญ
	- ถ้า Transaction ทั้งสอง ==แก้ไขข้อมูลชุดเดียวกัน== อาจจะเกิดปัญหาการชนกันได้ ==ลำดับจึงสำคัญ==
###### Recoverability
- ถ้า Transaction Fail ก็ต้องการันตีว่า Operation ต่าง ๆ ก่อนหน้านี้จะถูก Undo ทั้งหมด และจะถูก Mark จาก ส่วน Recovery ว่าถูก Rollback
- ถ้า Transaction Commit ก็ต้องถูกเขียนลงไฟล์และเขียนลง log file
- จากรูปจะเห็นว่า T2 มีการดึงข้อมูลจาก T1 แล้ว Commit ไปแล้วทำให้เป็น ==unrecoverable schedule== 
- ![Pasted image 20240306105735.png](./Pasted%20image%2020240306105735.png)
- F จะสังเกตได้ว่าข้อมูลที่ถูกต้องทั้งคู่ Commit ทั้งคู่ F2 ก็ตัดสินใจ Abort ทั้งคู่จึง Recover ได้ เรียกว่า ==Recoverable Schedule==
- ![Pasted image 20240306105923.png](./Pasted%20image%2020240306105923.png)
##### Concurrency Control Techniques
มีอยู่สองเทคนิคหลัก ๆ ( method )
- Locking
- Timestamping
ทั้งคู่เป็น conservative (or pessimistic) approaches :
- They cause transaction to be delayed when they conflict with other transactions
Optimistic approaches :
- Transaction conflict is rare. So they allow transactions to run unsynchronized and check for conflicts only when the transaction commits at the end
- ปล่อยให้แก้ไขไปเลย แล้วมาเช็คทีหลัง หากชน ก็ยกเลิกการ commit ทั้งคู่
###### Locking
- เป็นการล็อคข้อมูลไม่ให้ใครมาใช้ข้อมูลที่อยู่ในระหว่าง Transaction 
- จะพยายามล็อคให้น้อยที่สุด อาจจะถึงระดับ Row
- DBMS ส่วนใหญ่นิยมวิธีนี้
- จะไม่ยอมให้ Transaction อื่นเข้ามาแก้ไขหรือปลดล็อคข้อมูลที่ล็อคอยู่
- ทุกครั้งที่จบ Transaction ไม่ว่าจบแบบไหน ก็จะปลดล็อคข้อมูลอัตโนมัติ
- ระดับการล็อคจะขึ้นอยู่กับ DBMS ตัวอย่างเช่น Database -> Table -> Pages -> Record -> Column
Column
- ประเภทของ Lock
	- Shared Lock ( read Lock ) ( บางที่จะใช้คำว่า S Lock )
		- เกิดจากการอ่านข้อมูล
		- ทำให้อ่านพร้อมกันได้ แต่ไม่ยอมให้มีการแก้ไขข้อมูลหรืออัพเดท
	- Exclusive lock ( write lock )
		- Is used for write mode
		- มีแค่ Transaction ที่สั่งล็อคเท่านั้นที่ยุ่งกับข้อมูลได้
		- Transaction อื่นจะต้องรอจนกว่าจะมีการปลดล็อค
- Flowchart
- ![Pasted image 20240306111406.png](./Pasted%20image%2020240306111406.png)
#### Database Recovery
- To ensure that database is consistent when a failure occurs during
the transaction