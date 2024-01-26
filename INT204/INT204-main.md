#### Rest Api
- ทำหน้าที่ควบคุม resource
- แล้วรอให้ front-end มาเรียกใช้งาน
- แต่ละ method มีหน้าที่ที่แตกต่างกัน เช่น get ขอข้อมูล
- การสื่อสารกันระหว่าง Front-End และ Back-End นั้นต้องใช้ .json
- เราใช้ postman ในการทดสอบ api
- เวลาเราทำ Rest เราควรจะทำเป็น Layered System
	- Controller (Presentation Layer)
		- ทำหน้าที่คุยกับ Front-End
	- Service (Business Logic Layer)
		- ประมวลผล Logic ต่าง ๆ
	- Repository (Persistence Layer)
		- เข้าถึง Database
	- ต้องเรียกลงมาเรื่อย ๆ เท่านั้น ==**ห้ามข้าม!!!**==
#### Spring Boot
- เป็น Project ที่สร้างขึ้นมาครอบ Spring framework
	- หัวใจหลักของ Spring framework คือ Dependency injection
	- Spring framework + Embedded HTTP Server - XML Config = Spring Boot
- เขียน Config แค่นิดเดียว
- เอา Tomcat มาเป็นส่วนนึงไปเลย ไม่ต้องมานั่ง Deploy เอง
- สามารถสร้าง Stand-Alone application ได้
- จะไปตรวจสอบว่าเราใช้ library อะไรอยู่บ้างแล้วมันจะเข้าไป auto-config ให้เรา
- ทำไมต้องใช้ 
	- เป็น Dependency injection
	- ทำ Starter Project ให้เรา
- Spring Boot Architecture
	- Presentation Layer 
		- มีหน้าที่ติดต่อกับ Front-End
		- มีหน้าที่ในการ Authentication (คุณเป็นใคร)
	- Business
		- ทำ Authorisation (คุณมีสิทธิ์ทำอะไรบ้าง)
		- ทำ Validation
		- ทำ Business logic
	- Persistence 
		- ทำ Storage logic ก่อนส่งไป Database
	- Database 
		- ทำ CRUD
- Spring Web Annotation
	- มีการ mapping ว่าจะไปที่ class ไหน
		- ใช้ `@RequestMapping("<path>")`
		- แล้วค่อยไปแยก method ที่ส่งมาทีหลังเช่น `@GetMapping , @PostMappin\g`
	- มีการแปลง body เป็น object ของ java ให้ (`@RequestBody`)
		- เป็นการไปขอ Body มาให้ เราไม่ต้องเขียนการแปลงเอง
	- `@pathVariable` ขอดู pathVariable ได้
	- ![[../Pasted image 20240126114219.png|Pasted image 20240126114219]]
#### การใช้ h2.database 
- เพิ่ม Dependency และไป comment code ใน application.properties
	```
	<dependency>  
	    <groupId>com.h2database</groupId>  
	    <artifactId>h2</artifactId>  
	    <version>2.2.224</version>  
	    <scope>runtime</scope>  
	</dependency>
	```
- ทำไปเพื่อการทดสอบ Database เป็น database ใน main memory ไม่ใช่ database จริง ๆ
- เปิดปิด database นี้แล้วข้อมูลหายทันที
- ข้อมูลข้างในก็จะต้องเป็นไปตาม Constraint ของ Entity ที่เราเขียน
- ตอนเริ่มมาจะเป็น ```[]``` เพราะไม่มีข้อมูล แต่เชื่อมต่อ Database ได้แล้ว
- ดูข้อมูลได้ผ่าน
	- Postman
	- http://localhost:8080/h2-console
		- แล้วเอา ![[../Pasted image 20240126102840.png|Pasted image 20240126102840]] ใน terminal ไปใส่ใน JBDC:URL
		- สามารถตั้งเองได้เช่น `spring.datasource.url = jdbc:h2:mem:demo` ใน application.properties
	