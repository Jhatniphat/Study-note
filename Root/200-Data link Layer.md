##### Summary
การส่งข้อมูลในเลเยอร์นี้ จะมีทางเลือกได้หลายทาง (ไม่จำเป็นต้องส่งไปทางเดิมเสมอ) ปลายทางและต้นทางเวลาส่งกลับไปมาอาจจะไม่เหมือนกันได้
![Pasted image 20240123134031.png](./Pasted%20image%2020240123134031.png)
ถ้าอยากให้ไปในเส้นทางเดียวกันจะมีเทคโนโลยีให้ใช้
โดยการให้ตรวจสอบว่าเข้ามาที่พอร์อะไร แอพไหน แล้วให้ส่งไปออกทางไหน (กำหนดที่ Rounter) 
- ทำตารางขึ้นมา mapping
- ไม่ได้ออกแบบมาให้ใช้สำหรับ lan , ออกแบบมาให้ใช้กับ wan
- ลดความจำเป็นลงไปในปัจจุบันเพราะการมาก็ ip protocol
![Pasted image 20240123134120.png](./Pasted%20image%2020240123134120.png)

Layer 2 จะแบ่งออกเป็นสองส่วนคือ 
- Control
- MAC (media)

##### Data transfer 
[Data Transfer (Layer 2)](./Data%20Transfer%20(Layer%202).md)

##### MAC (Media Access Control)
Media ในที่นี้หมายถึง สายแลน สื่อสัญญาณ
Access Control ตัวควบคุมการรับส่ง

##### Multiple-access Protocol
![Pasted image 20240123134825.png](./Pasted%20image%2020240123134825.png)
หลายอุปกรณ์เข้ามาใช้ media ร่วมกัน จะเรียกว่า Multiple-access Protocol
[Multiple-access Protocol](./Multiple-access%20Protocol.md)

##### High-level Data Link Control
เป็น concept ของวิธีการตรวจสอบหรือวิธีการส่งข้อมูลต่าง ๆ ซึ่งส่วนใหญ่จะถูกนำไปปรับใช้เป็นส่วน ๆ ไม่ได้เกิดเป็นโปรโตคอลใหม่
![Pasted image 20240130135206](./Pasted%20image%2020240130135206.png)
ส่วนประกอบต่าง ๆ ใน frame 
- Flag - บอกหัวท้ายของ frame
- FCS - ใช้ทำ Error checking ย่อมาจาก Frame Check Sequence
- Address - ที่อยู่ของปลายทาง
- Control - เอาไว้ใส่คำสั่งควบคุมการสื่อสาร
- User information - ใส่ข้อมูลที่จะส่ง
	- ถ้ามีข้อมูลที่เหมือน flag ( 01111110 ) จะแก้ไขด้วยการแทรก 0 เข้าไป เช่น 011111010 ฝั่งผู้รับก็จะตัดศูนย์ที่โดยแทรกออก
ประเภทของ Frame
- I-frame มีข้อมูลที่ต้องการจะส่ง
- S-frame ไม่มีข้อมูลที่ต้องการจะส่ง แต่ต้องการควบคุมการสื่อสาร
- U-frame คล้าย ๆ s-frame แต่มีการเผื่อพื้นที่ไว้สำหรับคำสั่งยาว ๆ
###### PPP - Point to Point Protocol
Frame Format
- ![Pasted image 20240130140645](./Pasted%20image%2020240130140645.png)
- Protocal - บอกว่า Protocal ที่เรียกใช้ Protocal บน PPP คืออะไร เพราะว่าแต่ก่อนไม่ได้มีแค่ IP
- Padding คือส่วนที่ถูกเติมให้ขนาดมันพอดีกับที่จะส่งต่อให้การ์ดแลน ( จำนวน Bit )
###### Ethernet Frame
- ![Pasted image 20240130144634](./Pasted%20image%2020240130144634.png)
- Preamble ( flag ) จะมีขนาด 7 bytes เพื่อให้ผู้รับเตรียมตัว และจะไม่มี flag ตอนท้าย
- Ethernet เป็น Bus เลยต้องมี address ทั้ง Destination และ Source
- ใช้ check error แบบ CRC
- มีสิ่งที่เรียกว่า Jumbo frame เพราะให้ส่งข้อมูลได้เยอะ ๆ โดยที่ header เท่าเดิม
- ![Pasted image 20240130145135](./Pasted%20image%2020240130145135.png)
##### Wired Lan Ethernet
ด้วยความที่ว่าชื่อมาตรฐานมันจำยาก แล้วไม่สามารถบอกได้ว่าคืออะไรบ้าง เลยมีการออกชื่อมาใหม่
![Pasted image 20240130145515](./Pasted%20image%2020240130145515.png)
ซึ่งจะบ่งบอกว่าแต่ละชื่อ ใช้อยู่บนสายอะไร ระยะใช้งานเท่าไหร่
- ประเภทสาย
	- Multimode fiber
	- Singlemode fiber
	- Backplane
	- Cat.8
	- twinax copper cable
 - ชื่อเรียก
	 - LR - Long range
	 - ER - Extend range