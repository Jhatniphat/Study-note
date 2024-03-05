Architecture Styles - ภาพรวมใหญ่ ๆ ที่นิยมกัน
#### Architectural Style : foundations
##### Big ball of mud 
#Big_ball_of_mud 
- เป็นรูปแบบของแอพในสมัยก่อน ๆ ที่พันกันเป็นก้อน ๆ ยังไม่มีการออกแบบ Architecture
- ยกตัวอย่างเช่นมีการเรียกฟังก์ชันซ้ำซ้อนไปมา
##### Unitary architecture
#Unitary_architecture
- เป็นรูปแบบแอพที่ทำทุกอย่างในตัวยอ่างมันเอง 
- สังเกตได้ง่าย ๆ จะเป็น standalone app
- เช่น paint ( สร้างรูปแล้วเซฟไฟล์ จบในโปรแกรมเดียว ไม่ได้เรียก service จากที่อื่น)
##### Distributed architecture
#Distributed_architecture
- ตรงข้ามกับ Unitary
- ในแอพนึงจะมีหลาย ๆ ส่วนอยู่ด้วยกัน
- เป็นรูปแบบแอพในปัจจุบัน
- Client/server : desktop + DB , browser + web server , three-tier , etc.
- Monolithic style
- ข้อเสีย
	- อาจเกิดความผิดพลาดที่ Network
	- Network สามารถดีเลย์ได้ ควรจะรู้ถึง ค่าเฉลี่ยและค่าสูงสุดของ latency
	- Bandwidth มีขนาดที่จำกัด 
	- Network ไม่ Secure
	- Network อาจจะมีการเปลี่ยนแปลงได้ อาจจะส่งผลกระทบต่อ latency ของเราได้
	- Network บางส่วนอยู่นอกเหนือกันควบคุม เช่น Ais จะเปลี่ยนสายเน็ตตอนไหนก็ได้
	- Network มีราคาของมัน
	- Network อาจจะไม่ได้มาตรฐานมากพอ
##### Monolithic style
#Monolithic_style
- Layered architecture
	- แบ่งส่วนประกอบของแอพเป็นเลเยอร์ต่าง ๆ ![Pasted image 20240216154319.png](./Pasted%20image%2020240216154319.png)ในบางแอพ จะมีข้อกำหนดให้ไม่สามารถเรียกข้าม Layer ได้
	- ข้อดี
		- เหมาะกับแอพที่มีขนาดเล็ก simple app
		- เป็นรูปแบบสถาปัตยกรรมเริ่มต้นที่ดี
		- Low cost/time
		- Simple
- Pipeline architecture 
	- ให้นึกสภาพสายพาน ( ส่งต่อกันเป็นทอด ๆ )![Pasted image 20240216154926.png](./Pasted%20image%2020240216154926.png)
	- นิยมแบ่งฟังก์ชันออกเป็นสี่เรื่อง
		- Producers
		- Transformer
		- Tester
		- Consumer
		- ซึ่งจะแบ่งว่าส่วนไหนต้องทำอะไรก็ขึ้นอยู่กับแล้วแต่ Bussiness และ Logic
		- ข้อดี
			- เป็นการปบ่งทางเทคนิคที่ดี
			- Low cost/time
			- Simple
- Microkernel
	- ออกแบบมาเพื่อรองรับ plug-in component![Pasted image 20240216155700.png](./Pasted%20image%2020240216155700.png)
	- เช่น browser , linux
	- สามารถนำ Architecture Style อื่น ๆ มาผสมได้![Pasted image 20240216155750.png](./Pasted%20image%2020240216155750.png)
	- หรือบางที plug-in อาจจะอยู่ที่ UI![Pasted image 20240216160001.png](./Pasted%20image%2020240216160001.png)
	- มีระบบ Registry
		- ระบบขึ้นทะเบียน
		- มีไว้เพื่อให้ตัว Core สามารถรับรู้ได้ว่ามี plug-in อะไรอยู่บ้าง
		- รวมถึงการเลือกเปิด Service ให้ plug-in เรียกใช้ด้วยว่าเรียกอะไรได้บ้าง
		- ![Pasted image 20240216160203.png](./Pasted%20image%2020240216160203.png)![Pasted image 20240216160211.png](./Pasted%20image%2020240216160211.png)
	- มีระบบ Contract
		- มีข้อตกลงด้วยว่า plug-in นั้น ๆ มีสิทธิที่จะทำอะไรได้บ้าง << นึกถึงเวลาติดตั้งแอพมือถือจะบอกว่ามีสิทธิทำอะไรบ้าง
	- ข้อดีข้อเสีย
		- Low cost and simple 
		- มี modularity และ extendibility ที่สูง เพราะตัว Core จะมีขนาดเล็ก แต่สามารถเพิ่ม feature ได้จาก plug-in
		- มี testability และ deployability ที่สูง
##### Service-based architecture
#Service-based_architecture
- เป็น Microservices style architecture
- ไม่ซับซ้อน ( complex ) เท่า distributed architecture แบบอื่น
- แบ่งเป็น Layer ชัดเจน เช่น { UI > component > single DB } ![Pasted image 20240216162316.png](./Pasted%20image%2020240216162316.png)
- Single instance of each domain service
- ออกแบบได้หลากหลาย เช่นมีหลาย Ui หลาย DB ![Pasted image 20240216162445.png](./Pasted%20image%2020240216162445.png)
- สามารถมี API Layer ได้นะจ๊ะ![Pasted image 20240216162723.png](./Pasted%20image%2020240216162723.png)
- ตัวอย่าง![Pasted image 20240216162736.png](./Pasted%20image%2020240216162736.png)
- arch rating
	- Domain partitioned << domain-driven design
	- Agility
	- Testability
	- Deployability
	- ต้นทุนสูง
	- ![Pasted image 20240216163005.png](./Pasted%20image%2020240216163005.png)
	- Single DB ทำให้มีความสม่ำเสมอมากกว่า ( consistency )
	- เฉพาะบาง Service เท่านั้นที่สามารถ Scale ขึ้นได้
##### Event-driven architecture style
#Event-driven_architecture_style
- เป็น Asynchronous style
- มีตัวที่คอยรองรับแล้วกระจาย Request จาก User เรียกว่า Request Orchestrator ( บางครั้งอาจจะเป็นชื่ออื่นได้ )![Pasted image 20240216163654.png](./Pasted%20image%2020240216163654.png)
- บางครั้งก็ใช้เป็น Event แทน![Pasted image 20240216164136.png](./Pasted%20image%2020240216164136.png)
- มี Scalable , Performance ที่สูง
- สามารถผสมรวมกับ Style อื่นได้
- สามารถนำไปปรับใช้ได้ทั้ง Simple App และ Complex App ( แอพที่ซับซ้อน )
- arch rating
	- แบ่งเป็นส่วน ๆ ทางเทคนิคชัดเจน
	- มี Performance , scalability , fault tolerance
	- ไม่ simple
	- test ยาก
	- ![Pasted image 20240216165233.png](./Pasted%20image%2020240216165233.png)
##### Space-based architecture style
#Space-based_architecture_style
- เป็น Style ที่พยายามเพิ่มหน่วยประมวลผล ( Processing Unit ) เพื่อรองรับผู้ใช้งานที่เพิ่มมากขึ้น
- จากรูปจะเห็นได้ว่ามีการส่งต่อข้อมูลไปมา อาจจะทำให้เกิดข้อมูลที่ผิดพลาดเพราะข้อมูลของแต่ละตัวประมวลผลอาจจะไม่เหมือนกัน จึงเกิดขึ้นมาเป็น **==Data Replication Engine== เพื่ออัพเดทข้อมูลให้เหมือนกันในทุก ๆ ที่**![Pasted image 20240301153017](./Pasted%20image%2020240301153017.png)
- จะสังเกตจากรูปได้อีกว่ามี Database กลางในการจัดการร่วมกันอยู่ 
	- ใน Processing Unit จะใช้ memory ในการประมวลผล
	- เมื่อทำงานเสร็จหมดแล้ว จึงค่อยส่งเข้า Database เพื่อเก็บเป็นข้อมูลถาวร ( Permanent Storage )
	- Database ก็จะมีตัวช่วยที่คอยทำหน้าที่คอยอ่านข้อมูลและเขียนข้อมูล ก็คือ
		- Data Reader -> จัดการเรื่องข้อมูลตอนมีคำขอมา
		- Data Writer -> จัดการว่าใครเขียนได้บ้าง เขียนชนกันไหม 
- อีกแบบนึงคือ Processing Unit แต่ละส่วนทำงานแยก ๆ กัน ซึ่งก็จะมีตัวกลางคอยบริหารจัดการ คอยส่งและรอรับข้อมูลจาก Processing Unit![Pasted image 20240301153721](./Pasted%20image%2020240301153721.png)	- ปกติแล้วก็จะพยายามแจกงานให้สมดุล ( Balance ) กัน เรียกว่า Load Balancer 
- แบ่งออกเป็นหลาย ๆ ส่วน ยกตัวอย่างเช่น
	- Messaging Grid -> คอยรับส่งงานให้ Processing Unit , จัดลำดับคิวของ Process
	- Data Grid -> คอยจัดการข้อมูลให้ตรงกันอยู่เสมอ ๆ![Pasted image 20240301154127](./Pasted%20image%2020240301154127.png)
	- Processing Grid -> คอยจัดการการประมวลผล![Pasted image 20240301154405](./Pasted%20image%2020240301154405.png)
		- Deployment Manager -> มีหน้าที่ในการขอ Processing Unit เพื่มเมื่อมีโหลดเยอะเกินไป
	- บางที Style นี้ก็นิยมจะอยู่บน Cloud![Pasted image 20240301154544](./Pasted%20image%2020240301154544.png) ซึ่งจะสังเกตได้ว่า Database ก็สามารถจะอยู่ได้ทั้งในองค์กร และบน Cloud
- มีข้อดีคือมี Reliability , Performance , Scalability , Elasticity
- มีข้อเสียคือ ทดสอบยาก
##### Orchestration-driven Service-Oriented Architecture ( SOA )
#SOA #Orchestration-driven_Service-Oriented_Architecture 
- [SOA - Wikipedia](https://en.wikipedia.org/wiki/SOA)
- มีการพยายาม Reure!! service ต่าง ๆ
- ==ไม่ค่อยได้รับความนิยมมากนักในปัจจุบัน==
- เราจะพยายามจัดกลุ่มแยก Service ต่าง ๆ ให้แยกออกมา![Pasted image 20240301155604](./Pasted%20image%2020240301155604.png)
- มีแนวคิดที่ว่า ไม่ว่าจะงานไหน ๆ หรือ service ไหน ๆ ก็จะต้องมีใช้ service พื้นฐาน เช่น Infrastructure Services
- ###### SOA Component
	- Business services
		- ทำหน้าที่หลักในการตอบสนองความต้องการทางธุรกิจ
		- ประกอบไปด้วยชุดของฟังก์ชันการทำงานที่เกี่ยวข้องกัน
		- **ตัวอย่าง**: บริการจัดการลูกค้า บริการจัดการสินค้าคงคลัง
	- Enterprise services
		- มุ่งเน้นไปที่การสนับสนุนการทำงานของ Business Services
		- นำเสนอบริการพื้นฐานที่ใช้ร่วมกัน เช่น การจัดการความปลอดภัย การจัดการธุรกรรม
		- **ตัวอย่าง**: บริการการตรวจสอบสิทธิ์ บริการจัดการคิวข้อความ
	- Application services
		- ทำหน้าที่เป็นตัวกลางเชื่อมต่อระหว่าง Business Services กับ Enterprise Services
		- จัดการการทำงานที่ซับซ้อนโดยใช้ Business Services หลายตัว
		- **ตัวอย่าง**: บริการตะกร้าสินค้า บริการการชำระเงิน
	- Infrastructure services
		- มุ่งเน้นไปที่การจัดการทรัพยากรระบบพื้นฐาน
		- นำเสนอบริการพื้นฐาน เช่น การเข้าถึงฐานข้อมูล การเชื่อมต่อเครือข่าย
		- **ตัวอย่าง**: บริการฐานข้อมูล บริการเครือข่าย
	- Orchestration services
		- ทำหน้าที่ควบคุมการทำงานของ Business Services หลายตัว
		- กำหนดลำดับขั้นตอนและเงื่อนไขในการทำงาน
		- **ตัวอย่าง**: เครื่องมือ Business Process Management (BPM)
- ###### SOA ratings
	- มีข้อดีคือ Scalability เพราะสามารถ Scale เป็นส่วน ๆ ได้
	- มีข้อเสียคือ complex , hard to set
##### Microservice architecture
#Microservice_architecture
- แยก service ออกเป็นส่วน ๆ ตาม Business domain โดยหวังว่าจะคุยข้ามกันให้น้อยที่สุด 
- เปลี่ยนแปลงไปตาม trend ได้ง่าย สมมุติส้มกำลังมา ก็ใช้ส้ม พอส้มไป ก็เปลี่ยนไม่ใช้แบบอื่นเช่น เขียวแทน
- มี Database แยกออกไปในแต่ละ Service![Pasted image 20240301162855](./Pasted%20image%2020240301162855.png)
- ต้องจัดการเรื่อง Choreography -> อาจจะต้องรวมบาง Service เข้าด้วยกัน
- อาจจะเกิดข้อมูลในฐานข้อมูลไม่ตรงกัน
- บางทีอาจจะมีโค้ดบางส่วนที่ไปแปะในหลาย ๆ Service เรียกว่า ==side-car== เช่น monitoring , logging![Pasted image 20240301163242](./Pasted%20image%2020240301163242.png)
- Micro Service ก็อาจจะมีการใช้ Choreography ( ซ้าย ) และ Orchestration ( ขวา )![Pasted image 20240301163825](./Pasted%20image%2020240301163825.png)
##### Serverless Architecture
#Serverless_Architecture
- พอเริ่มมี Cloud มากขึ้น ก็เริ่มมีแนวคิดนี้ขึ้นมา
- เราทำ front-end เอง แต่ back-end และ database ก็ใช้ service ของคนอื่น
- **ตัวอย่าง** : เราทำ front-end เอง แต่ back-end ใช้ service lazada และ database ก็ใช้ service ของ amazon![Pasted image 20240301164641](./Pasted%20image%2020240301164641.png)