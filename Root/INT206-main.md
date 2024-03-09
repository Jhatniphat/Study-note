Advanced Database
[Query processing](./Query%20processing.md)
[Database Security and Administration](./Database%20Security%20and%20Administration.md)
[Transaction Management](./Transaction%20Management.md)
#### Database design stages
![Pasted image 20240123233355.png](./Pasted%20image%2020240123233355.png)
- Conceptual Database Design
	- ไม่ยึดติดกับ DBMS ที่เลือกใช้
	- ต้องเห็นว่าจะเก็บข้อมูลอะไรบ้าง (ไม่ต้องลงรายละเอียดเยอะ เอาที่ User เข้าใจได้)
- Logical Database Design
	- ลงดีเทลว่าเก็บอะไรบ้าง ยังไง datatype
- Physical Database Design
	- เก็บ Data ยังไง (How is the data assessed/stored)
	- [Physical Database Design](./Physical%20Database%20Design.md)
Logical design vs Physical design
	- Logical จะมุ่งเน้นไปที่การแปลงการ Conceptual ในกลายเป็น Data model  แบบ relational model
	- Physical จะมุ่งเน้นไปที่ประสิทธิภาพการเข้าถึงของข้อมูล
#### Query processing
เป็นกระบวนการตั้งแต่เริ่มจนจบของการ query 
ต้องเช็ค syntax เช็คข้อมูลว่ามีจริงมั้ย เช็คว่ามีสิทธิมั้ย
[Query processing](./Query%20processing.md)

[Database Security and Administration](./Database%20Security%20and%20Administration.md)

