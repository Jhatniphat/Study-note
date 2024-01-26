#### **Summary**
- เป็นขั้นตอนสุดท้ายของการ Design Database 
- แปลงจาก Logical Design ให้มี การดำเนินการที่มีประสิทธิภาพ (an efficient implementation)
- มุ่งเน้นไปที่ประสิทธิภาพการทำงานของ Database
#### **Defination**
- Process of producing a description of the implementation of the database on secondary storage 
- Describe: 
	- Base relations (derived data, general constraints) (ความสัมพันธ์ระหว่างข้อมูลและข้อกำหนดของข้อมูล)
	- File organization (การจัดการไฟล์)
	- Indexes 
	- Query optimization (ประสิทธิภาพการเข้าถึง)
	- Security measures (ความปลอดภัยของข้อมูล)
#### Derived data
- เป็น Attribute ที่เกิดมาจากการคำนวณของ Attribute อื่น ๆ
- Ex. จำนวนพนักงานทั้งหมดในสาขานั้น ๆ
- มีอยู่สองตัวเลือกในการเก็บ Derived Data คือ
	- Store (เก็บค้างไว้เป็น Attribute หนึ่งไปเลย)
		- ทำให้เปลืองพื้นที่จัดเก็บ , ข้อมูลอาจจะเก่า
		- เหมาะกับการสรุปยอดราคาในบิล
		- มีประสิทธิภาพมากกว่าการคำนวณใหม่ทุกครั้ง
	- Calculate (คำนวณใหม่ทุกครั้งที่ต้องการใช้)
		- ข้อมูลทันสมัยกว่า (Up to date)
		- มีประสิทธิภาพน้อยกว่าแบบ Store
		- ประหยัดพื้นที่จัดเก็บได้
#### General constraints
- มีรูปแบบที่เห็นได้ทั่วไปดังนี้
	- Integrity constraint (Primary key)
	- Required data (Not NULL)
	- Check constraint (ใส่เงื่อนไข)
	- Referential constraint (Foreign key)
	- Unique constraint (ห้ามซ้ำ)
- ควรควมคุม constraint ที่ไหน
	- ควรควบคุมที่ Database เพราะโอกาสผิดพลาดน้อย หากไปควมคุมที่ Application จะทำให้เกิดข้อผิดพลาดได้ง่าย เพราะจำเป็นต้องเขียนการควบคุมหลาย ๆ ส่วน

#### File organization
- เป็นสิ่งที่สำคัญมากใน Physical Database Design
- มีวัตถุประสงค์ไปที่การจัดเก็บและเข้าถึงข้อมูลได้อย่างมีประสิทธิภาพ
- ประเภทของ File organization จะขึ้นอยู่กับ DBMS ที่ใช้
- การวิเคราะห์
	- จุคประสงค์ของ Database นั้น ๆ
	- DBMS ที่เลือกใช้
	- ดูที่ Transactions
		- เกิด transactions อะไรบ่อยที่สุด
		- เกิดในช่วงเวลาไหนมากที่สุด
		- สนใจแค่ 20% ที่มีการ Active มากที่สุดแทนการสนใจทั้งหมด
	ยังจดไม่หมดจ้า
#### Index?
- เป็นสิ่งที่ทำให้เราเข้าถึงข้อมูลได้เร็วและมีประสิทธิภาพมากขึ้น
- เปรียบเทียบได้กับ index ในหนังสือ ที่ช่วยให้เราค้นหาสิ่งที่เราสนใจได้เร็วขึ้น (ต่างจากสารบัญตรงที่ว่า index จะเรียงตามตัวอักษรแต่สารบัญจะเรียงตามเนื้อหาในหนังสือ)
- ใช้พื้นที่เพิ่ม (ถือเป็นไฟล์เพิ่มอีกหนึ่งไฟล์)
- ต้องมีความสัมพันธ์กับข้อมูล
- ใน DBMS จะมี optimizer ในการตัดสินใจว่าจะใช้ index หรือไม่
- ลำดับของ column เวลา index นั้น ๆ มีหลาย column มีความสำคัญ เช่น (countryCode , Language) หากเราค้นหาด้วย countryCode จะมีการเรียกใช้ index แต่ถ้าค้นหาด้วย Language จะไม่ถูกเรียกใช้ เพราะความสำคัญจะอยู่ที่ column แรกเสมอ เราเรียกกฎข้อนี้ว่า ==Leftmost Index Prefixes==
- โครงสร้างของอินเดกซ์
	- จะเก็บข้อมูล key value 
	- เก็บ Address ของข้อมูลว่าอยู่ที่ไหน (Address of logical records)
- ข้อมูลในอินเดกซ์ต้องจัดเรียงเสมอ
- ประเภทของ Index
	- Primary Index
		- สร้างจาก key field จึงทำให้การันตีว่าเป็น Unique
		- ข้อมูลใน Data file จะต้องจัดเรียงเท่านั้น
	- Clustering Index
		- สร้างจาก non-key field 
		- สามารถซ้ำกันได้
		- เกิดจากการสร้าง index บน column ที่ซ้ำกันได้
		- ข้อมูลใน Data file จะต้องจัดเรียงเท่านั้น
		- ![Pasted image 20240124095237.png](./Pasted%20image%2020240124095237.png)
		- ![Pasted image 20240124095346.png](./Pasted%20image%2020240124095346.png)
	- Secondary Index
		- สร้างจาก non-ordering field
		- สร้างเพิ่มโดยที่ไม่มีผลอะไรกับ Data file
		- ข้อมูลใน Data file ไม่จำเป็นต้องจัดเรียง
		- เพื่อเพิ่มความเร็วในการ query
		- มี Overhead
			- มีการเลือก node ที่จะแทรกหรือแก้ไขทุกครั้งที่มีการแก้ไขหรือเพิ่มข้อมูล
		- ไม่ควรจะมีการแก้ไขข้อมูลบ่อย ๆ
	- ใน 1 ไฟล์ต้องเลือกระหว่าง 1 Primary Index หรือ 1 Clustering Index
		- Secondary Index จะมีกี่ตัวก็ได้ ขึ้นอยู่กับการใช้งาน
- Sparse vs Dense
	- ![Pasted image 20240124094700.png](./Pasted%20image%2020240124094700.png)
	- A คือ Dense
		- เอาทุกค่าใน Data file มาเก็บใน Index
	- B คือ Sparse
		- เลือกมาบางค่ามาเก็บใน Index
	- ปกติแล้วเวลาสร้าง DBMS จะจัดการให้เรา
- Guideline for choosing indexs
	- Do not index small relations (ถ้าตารางข้อมูลมันไม่เยอะ ก็ไม่จำเป็นต้องสร้าง)
	- เวลาที่ระบุว่า column ไหนเป็น PK ระบบจะสร้าง Index ให้อัตโนมัติ
	- ควรจะเพิ่ม Index ใน FK เพราะเราจะ query ได้เร็วขึ้นตอน join
	- Attribute ใดก็ตามที่มีการใช้งานบ่อย ๆ เรามักจะสร้าง Index บน Attribute นั้น
		- ดูได้จากเรา where clause , order by , group by ด้วย column อะไรบ่อย ๆ
	- เราสามารถสร้าง index ด้วย function ( built-in aggregate function or built-in function ) ได้
		```
		Select branchno, avg(salary) From staff Group by branchno ; 
		Create index staff_sal_idx on staff(branchno,salary) ;
		```
		การสร้าง index แบบนี้จะทำให้เกิดสิ่งที่เรียกว่า index-only plan เพราะอ่าน index แล้วสามารถนำไปประมวลผลได้เลย โดยที่ไม่ต้องไปอ่าน Data file
	- ไม่ควรสร้างใน column ที่มีการอัพเดทบ่อย ๆ
	- ไม่ควรสร้างใน column ที่มีการ query แล้ว return row จำนวนมาก ๆ
	- ไม่เหมาะการ column ที่ Data ค่อนข้างมีความยาว
	- ถ้าเป็น few values (low cardinality) เช่นเพศ สถานะ ควรจะสร้างเป็น bitmap indexes
	- ไม่ใช่ว่าการสร้าง index บนหลาย ๆ column จะดีเสมอไป เพราะการสร้าง index บนหลาย ๆ column ตอนใช้งานจะต้องใช้งานตรงตามจุดประสงค์ของมันจริง ๆ มันถึงจะถูกเรียกใช้ เช่น เราสร้าง index ที่มี ชื่อ,ชั้นปี,ภาควิชา ตอนใช้งานก็ต้องใช้ให้เครบสามตัว ระบบถึงจะเรียกใช้
- B-Tree 
	- ย่อมาจาก Binary Tree
	- หลาย ๆ DBMS นิยมใช้
	- Characteristics
		- Balanced มีความสมดุล leaf แต่ละจุดจะมีความลึกที่เท่า ๆ กัน
		- Bushy
		- Block-oriented
		- Dynamic มีความยืดหยุ่น
	- แบบจำลอง [B-Tree Visualization (usfca.edu)](https://www.cs.usfca.edu/~galles/visualization/BTree.html) 
	- B+-Tree vs B-Tree
		- B+-Tree นำข้อมูลของ root node มาเก็บไว้ที่ leaf node ด้วย ทำให้ข้าม node ได้ง่ายขึ้น
		- ![Pasted image 20240124104842.png](./Pasted%20image%2020240124104842.png)
		- B-Tree เวลาข้าม node จะต้องวิ่งขึ้นไปยัง parent node เพื่อข้าม node
		- ![Pasted image 20240124104852.png](./Pasted%20image%2020240124104852.png)
- Bitmap indexes
	- นิยมใช้กับ Data warehouse เพราะเป็นข้อมูลที่นิ่งแล้ว
	- โดยทั่วไปเวลาสร้างจะเป็นแบบ sparse
	- มีทุกอย่างเหมือน index ปกติ แต่จะมีการเก็บ bit ตามจำนวน row
		- ถ้า bit เป็น 0 แสดงว่าไม่ match
		- ถ้า bit เป็น 1 แสดงว่า match
		- ![Pasted image 20240124105401.png](./Pasted%20image%2020240124105401.png)
		- หลักใน bitmap = ลำดับของ data 
- join indexes
	- เป็นการสร้าง index บน Attribute ที่มาจากหลาย Relation
	- นิยมใน Data warehouse
	- ![Pasted image 20240124110133.png](./Pasted%20image%2020240124110133.png)
	- ในรูปข้างต้น สมมุติว่า เวลาอ้างถึง London ( city ) จะไปเกี่ยวข้องกับ row ( ของทั้งสองตาราง ) ไหนบ้าง
	- เน้นไปที่การเข้าถึงข้อมูลได้เร็วขึ้น
- cluster and non-clustered table
	- Clustered tables 
		- เป็นการ group ข้อมูลที่มันเกี่ยวข้องจากหลายตาราง
		- เอาข้อมูลที่มันเกี่ยวข้างกันมาเก็บด้วยกันใน physical ด้วยกันเลย ทำให้เข้าถึงข้อมูลได้เร็วขึ้น
		- ![Pasted image 20240124110814.png](./Pasted%20image%2020240124110814.png)
		- จากรูปตัวอย่าง ทุกครั้งที่เราจะใช้ข้อมูล Branch เราก็จะเรียก Employee มาด้วยเลย ฉะนั้นเราจึงสร้าง Clustered table มาไว้ โดยใช้ branchNo เป็น Cluster Key
		- การเก็บข้อมูลจะเป็นแบบนี้
		- ![Pasted image 20240124111055.png](./Pasted%20image%2020240124111055.png)
	- non-clustered table
		- ปกติเวลาสร้าง table จะเป็น non-clustered table
- การใช้งาน
	- การใช้คำสั่ง Explain ว่ามีการใช้ index หรือไม่
		- ![Pasted image 20240124114727.png](./Pasted%20image%2020240124114727.png)
		- ถ้ามีการใช้งาน Index จะขึ้นที่ column key ถ้าไม่ใช้จะขึ้นเป็น null
		- ![Pasted image 20240124114908.png](./Pasted%20image%2020240124114908.png)
	- การสร้าง Index
		```
		create index <index-name> on <table-name> ( <column-name> );
		```
	- การเช็คว่าตารางนี้มี Index อะไรบ้าง
		```
		show index from <table-name>;
		```
		- ![Pasted image 20240124115534.png](./Pasted%20image%2020240124115534.png)
#### Denormalization
- ตรงข้ามกับการ Normalization เพราะ
	- การ Normalization ทำให้ต้อง join หลายครั้ง
	- แต่มีข้อดีที่ประหยัดพื้นที่ของข้อมูล
- เราอาจจะเลือกทำ Denormalization ในบางจุดหรือบางตาราง
- ทำเพื่อความเร็วหรือ Performance เป็นหลัก
- แลกมากับการเก็บข้อมูลซ้ำซ้อน การเก็บหลาย ๆ ที่
- การทำ Denormalization
	- ปรับโครงสร้างตารางเดิม
		- การเก็บข้อมูลเพิ่มเพื่อเก็บข้อมูลซ้ำ
	- สร้างตารางใหม่เพิ่ม
		- รวมตารางหลาย ๆ ตารางเข้าด้วยกัน
		- เหมาะกับการสร้างตารางสำหรับการออกรีพอร์ต ( โอกาสที่จะถูกแก้ไขข้อมูลน้อย ) รวมถึงตารางที่เป็นประวัติ
- เกณฑ์ในการเลือกทำ
	- Performance ยังไม่เป็นที่น่าพอใจ
	- ตารางนั้นมีการ Update บ่อยหรือไม่ ถ้าบ่อยก็ไม่เหมาะ
	- ถูก query บ่อยหรือไม่ ถ้าบ่อยก็เหมาะ