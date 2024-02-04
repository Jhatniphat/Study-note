[Linux cli](./Linux%20cli.md)
[Process](./Process.md)
#### Software Architecture Foundation
##### Software Architecture?
###### Architecture Styles - ภาพรวมใหญ่ ๆ ที่นิยมกัน
###### LAW of SW Arch
- ทุกอย่างใน Software Architecture จะมี Trade-off (มีสิ่งที่จะต้องแลกเปลี่ยน)
	- เช่นการแตะบัตรเข้าตึก lx ที่เป็นเกี่ยวกับความมั่นคง เราต้องยอมเปิดประตูทิ้งไว้เพื่อลดความแออัด
	- เราจำเป็นต้องคำนึงถึงปัจจัยอื่น ๆ ที่อาจจะขัดแย้งกันได้
	- ถ้าเราเป็น SW Architect เราต้องอธิบายให้ได้ว่าทำไมเราถึงทำแบบนี้ แล้วก็ต้องปรึกษาด้วยว่าทำได้ไหมหรืออะไรยังไง
- เราควรจะมีเหตุผลว่าทำไมเราถึงต้องเลือกอันนี้ สำคัญกว่าทำยังไง
###### Arch vs design
![Pasted image 20240126155024.png](./Pasted%20image%2020240126155024.png)
###### Arch vs Dev (person)
![Pasted image 20240126155223.png](./Pasted%20image%2020240126155223.png)
- ซ้าย - Developer
- ขวา - Architecture
###### Structure
- มองว่าใช้ Architecture Styles อะไร
Architecture Characteristics
- คุณสมบัติต่าง ๆ ของ Architecture
Design Principles
- ข้อมูลรายละเอียดในแต่ละเรื่องย่อย ๆ
- นิยมทำแบบ async messaging เพื่อเพิ่ม performance
	- ไม่จำเป็นต้องรอ response อยู่เสมอ ๆ สามารถไปทำอย่างอื่นรอได้
	- เป็น Decisions (อาจจะต้องมาทบทวน เพราะไม่สามารถทำได้ในทุกส่วน)
Decisions vs Principles
- ถ้าเราจะไม่ทำตาม Decisions อาจจะต้องพิจารณาถึงคณะกรรมการ
- แต่ Principles อาจจะพิจารณาถึงหัวหน้าทีมในฝ่ายนั้น ๆ
