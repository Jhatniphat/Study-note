###### Data transfer (Layer 2)
การส่งข้อมูลเราจะส่งเป็น Frame 
![Pasted image 20240123150147.png](./Pasted%20image%2020240123150147.png)
ระหว่างทางตรงกลางห้ามส่งเป็น  01111110 เพราะผู้รับจะคิดว่าข้อมูลสิ้นสุดแล้ว
เรื่องที่เราควรสนใจ
	- ขนาดของ Frame 
		- ปริมาณข้อมูลที่ออกไป = bps ( bit per second )
	- Flow ของข้อมูล
		- มีการบันทึกการเข้าคิวของ data ที่ตัว switch
		- ถ้าข้อมูลมันเข้ามาเร็วมาก ๆ จน Buffer ของ switch มันเต็ม เลเยอร์ 2 ก็จะทิ้งเลย
		- เราจึงต้องบริหารจัดการให้ไม่มากไปไม่น้อยไป
		- ใน lan จะไม่ค่อนสนใจ เพราะส่วนใหญ่ความเร็วจะเท่านั้นหมด

![Pasted image 20240123151735.png](./Pasted%20image%2020240123151735.png)
การตรวจสอบ Error ระหว่างการส่งข้อมูล จะใช้เทคนิคที่เรียกว่า CRC ( Cyclic Redundancy Check )
- ตรวจพบ Error ของข้อมูลได้เกือบทั้งหมด
- ทำในการ์ด Lan (Hardware)
- ดูซับซ้อนแต่คำนวณง่าย