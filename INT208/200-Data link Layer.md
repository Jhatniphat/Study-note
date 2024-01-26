##### Summary
การส่งข้อมูลในเลเยอร์นี้ จะมีทางเลือกได้หลายทาง (ไม่จำเป็นต้องส่งไปทางเดิมเสมอ) ปลายทางและต้นทางเวลาส่งกลับไปมาอาจจะไม่เหมือนกันได้
![[../Resource/image/Pasted image 20240123134031.png|Pasted image 20240123134031.png]]
ถ้าอยากให้ไปในเส้นทางเดียวกันจะมีเทคโนโลยีให้ใช้
โดยการให้ตรวจสอบว่าเข้ามาที่พอร์อะไร แอพไหน แล้วให้ส่งไปออกทางไหน (กำหนดที่ Rounter) 
- ทำตารางขึ้นมา mapping
- ไม่ได้ออกแบบมาให้ใช้สำหรับ lan , ออกแบบมาให้ใช้กับ wan
- ลดความจำเป็นลงไปในปัจจุบันเพราะการมาก็ ip protocol
![[../Resource/image/Pasted image 20240123134120.png|Pasted image 20240123134120.png]]

Layer 2 จะแบ่งออกเป็นสองส่วนคือ 
- Control
- MAC (media)

##### Data transfer 
[[./Data Transfer (Layer 2)|Data Transfer (Layer 2)]]

##### MAC (Media Access Control)
Media ในที่นี้หมายถึง สายแลน สื่อสัญญาณ
Access Control ตัวควบคุมการรับส่ง

![[../Resource/image/Pasted image 20240123134825.png|Pasted image 20240123134825.png]]
หลายอุปกรณ์เข้ามาใช้ media ร่วมกัน จะเรียกว่า Multiple-access Protocol
[[./Multiple-access Protocol|Multiple-access Protocol]]


