[Linux cli](./Linux%20cli.md)
[Process](./Process.md)
[Ubuntu Package Management and Service Managers](./Ubuntu%20Package%20Management%20and%20Service%20Managers.md)
#### Software Architecture Foundation
##### [Architecture Characteristics](./Architecture%20Characteristics.md)
[Software Architecture Style](./Software%20Architecture%20Style.md)
##### Software Architecture?

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
- [Architecture Characteristics](./Architecture%20Characteristics.md)
Design Principles
- ข้อมูลรายละเอียดในแต่ละเรื่องย่อย ๆ
- นิยมทำแบบ async messaging เพื่อเพิ่ม performance
	- ไม่จำเป็นต้องรอ response อยู่เสมอ ๆ สามารถไปทำอย่างอื่นรอได้
	- เป็น Decisions (อาจจะต้องมาทบทวน เพราะไม่สามารถทำได้ในทุกส่วน)
Decisions vs Principles
- ถ้าเราจะไม่ทำตาม Decisions อาจจะต้องพิจารณาถึงคณะกรรมการ
- แต่ Principles อาจจะพิจารณาถึงหัวหน้าทีมในฝ่ายนั้น ๆ
###### Measuring architecture
- Ex.
	- เวลาพูดถึง Agility , Deployability <<< เราควรจะมาคุยว่าเราต้องทำอะไรบ้าง วัดยังไง
	- Multiple meaning/aspect บางอย่างมีหลายมุมมอง หลากความหมาย <<< หา common definition
- หา objective(วัดได้) definitions ที่ทุกคนยอมรับได้
- Operational measures 
	- Performance
		- Response time ( ค่าเฉลี่ย นานสุดของเวลาตอบสนอง )
		- First page render time ( เวลาเรนเดอร์ของหน้าแรก )
	- Scalability
		- วัดว่าการใช้งานแบบเรียลไทม์เหมาะสมหรือไม่
		- System can still serve XXX more users/transactions ( ระบบสามารถตอบสนองต่อจำนวน User เท่า ... ได้หรือไม่ )
- Structural measures
	- ตรวจสอบ Code structure ว่าเขียนไว้ได้ดีหรือไม่
		- Ex. cyclomatic complexity (CC) ( ผู้เขียนหนังสือบอกว่าไม่ควรเกิน 5 ) << ค่าความซับซ้อนในตัววงวรหรือไซเคิล มีผลต่อ Maintainability ด้วย
		- มีเครื่องมือตรวจสอบอยู่ในหลาย ๆ ภาษา
		- การเขียนแบบ Test-driven development จะช่วยในเรื่องนี้ได้ ( คิดวิธีทดสอบมาก่อนจะช่วยให้มี Deflect ที่น้อยกว่า )
- Development Process measures
	- Agility 
		- Deployability
			- เปอร์เซนการ Deploy สำเร็จ
			- issues/bugs ที่เจอในระหว่างการ Deploy
			- เวลาในการ Deploy
		- Testability
			- code coverage? >> How much your code is tested
			- [What is Code Coverage? | Atlassian](https://www.atlassian.com/continuous-delivery/software-testing/code-coverage)
	- เลือกตัววัดซักชุดที่เก็บข้อมูลที่เป็นประโยชน์กับโปรเจคของเรา
- Governance and fitness functions
	- เอาตัววัดต่าง ๆ มาประกบรวมกัน >> เรียกว่า fitness function![Pasted image 20240209161302.png](./Pasted%20image%2020240209161302.png)
		- Chaos engineering เป็นเทคนิคการดูที่ความวุ่นวายของระบบ
		- Unit Test เป็นการทดสอบการทำงานของแต่ละ Module
	- Architecture Governance >> พยายามทำให้มั่นใจว่าเราผ่าน fitness function
		- Governance > การควบคุม , การกำกับดูแล
###### Component
- Component ในระดับสถาปัตยกรรม หมายถึงตัว Module ที่ออกมาในเชิงกายภาพแล้ว
- Application หนึ่ง อาจจะมีหลาย ๆ Component
- บางครั้งขอบเขตก็รวมถึง Library และ Service ด้วย
- Architecture Quantum
	- ในหนึ่งขอบเขตอาจจะมีได้หลาย ๆ Component
	- Ex. เราจะดู Performance ของ quantum นี้
	- เราคาดหวังว่าใน Quantum นั้น ๆ จะเป็นเรื่องที่มีความสัมพันธ์กัน
	- แต่ละ Quantum สามารถ Deploy โดยอิสระจากกันได้
- ตัวอย่างการมอง Component ในรูปแบบต่าง ๆ ![Pasted image 20240209163204.png](./Pasted%20image%2020240209163204.png)
- จะแบ่งละเอียดหรือมากน้อยแค่ไหน ก็แล้วแต่ความเหมาะสม ไม่มีวิธีที่ตายตัว
- Partitioning
	- แนวคิดในการแบ่งเป็นส่วน ๆ ซึ่งจะมีอยู่สองแนวคิดหลัก ๆ คือ
		- Domain แบ่งตาม Workflow หรือ function ทางธุรกิจ
			- ข้อดี
				- ใกล้เคียงกับวิธีการทำงานในธุรกิจนั้น ๆ อยู่แล้ว เพราะแบ่งตาม function ทางธุรกิจ
				- ไปในทางเดียวกันกับ microservice กับ modular monolith
				- บริหารจัดการ Flow ง่ายเพราะเป็นไปตาม Domain เดิม
				- การแยกข้อมูลออกไปในแต่ละ service มันจะง่ายกว่า
			- ข้อเสีย
				- โค้ดที่มีการ Customization มันก็จะอยู่ได้แค่ module นั้น ๆ เลย
			- ![Pasted image 20240209164629.png](./Pasted%20image%2020240209164629.png)
		- Technical แบ่งตามเทคนิคที่เลือกใช้ เช่น MVC
			- ข้อดี
				- ง่ายต่อการ Customization
				- เป็นไปในทางเดียวกันกับการแบ่งแบบ Layer ต่าง
			- ข้อเสีย
				- ถ้าเราไปแก้ไขหรือทำอะไรใน Layer หนึ่งก็จะส่งผลต่อ Layer อื่นด้วย
				- การดำเนินการทางธุรกิจก็จะต้องวิ่งผ่านทุก Layer
				- มี coupling ที่สูงกว่า
			- ![Pasted image 20240209164644.png](./Pasted%20image%2020240209164644.png)
	- ![Pasted image 20240209163530.png](./Pasted%20image%2020240209163530.png)
	- การเลือกเทคนิคการแบ่ง
		- พยายามดูก่อนว่าในจุดเริ่มต้นจำเป็นต้องมี Component อะไรบ้าง
		- ดู Characteristic ว่ามีอะไรบ้าง
		- หาวิธีทำสิ่งต่าง ๆ ตาม Characteristic
		- ![Pasted image 20240209164944.png](./Pasted%20image%2020240209164944.png)


#### UML (Unified Modeling Language)
- เป็นแนวทางหรือรูปแบบของ Diagram ที่เป็น มาตรฐานเดียวกัน
- เพื่อให้สื่อสารระหว่างกันง่ายขึ้น
- มีอยู่หลายแบบมากเช่น Class Diagram , Component Diagram , [Activity diagram](https://creately.com/blog/diagrams/activity-diagram-tutorial/) , [Sequence diagram](https://creately.com/blog/diagrams/the-basics-the-purpose-of-sequence-diagrams-part-1/) , [Usecase-Diagram](https://creately.com/blog/diagrams/use-case-diagram-relationships/)
- 