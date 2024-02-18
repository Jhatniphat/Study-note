Network II

Layer
- [200-Data link Layer](./200-Data%20link%20Layer.md)
LAB
- [Virtual local area network](./Virtual%20local%20area%20network.md)

#### Summary
##### TCP/IP Protocol
- ![Pasted image 20240213134357.png](./Pasted%20image%2020240213134357.png)
- ARP คือ การถามรายละเอียดเช่น Ip address , Mac address 
- SSL หรือ TLS ทำหน้าที่ Encrypt ข้อมูล จะแทรกอยู่ระหว่าง Layer 4 กับ Layer 5
- ใช้ DNS ไปหา ip แล้วส่งให้ Layer ล่าง ๆ ( Layer 3)
- ละก็ไปหา Mac ต่อ เพื่อส่งให้ Layer 2
- วิธีการหา ip address ว่าอันนี้ของใคร ? 
	- จะใช้การตะโกน (Broadcast) หา![Pasted image 20240213134829.png](./Pasted%20image%2020240213134829.png)
	- ตอนตอบกลับก็จะตอบไปที่คนถามคนเดียว ไม่ได้ Broadcast แล้ว
- ARP Packet![Pasted image 20240213134954.png](./Pasted%20image%2020240213134954.png)
	- กรณีที่ไม่รู้ MAC address จะปล่อยให้เป็น 000000000 ใน Destination hardware address
	- ในรูปข้างต้น ทั้งหมดมีขนาดรวม ๆ 24 byte ( 1 บรรทัด = 4 byte ) เพราะไม่ได้ทำอะไรมาก แค่ถามหา Mac address
	- Hardware Length กับ Protocol Length จะบอกว่าให้อ่าน Address กี่ Byte
- การข้ามวงของ Network![Pasted image 20240213140411.png](./Pasted%20image%2020240213140411.png)
	- จะต้องวิ่งผ่าน Gateway ไปเรื่อย ๆ
	- จากเครื่องต้นทางไปจนถึงปลายทางก็จะมีการถามหา ARP เรื่อย ๆ ตลอดทาง ( ทั้งขาไปและขากลับ )
- L2 (Data Link Layer)
	- แบ่งเป็นสองส่วนคือ
		- Logical Link
			- LLC ทำเรื่อง Virtual Circuit ( อยากให้วิ่งยังไง ) << แล้วแต่ App ว่าจะใช้ไหม ถ้าไม่ใช้ก็ใช้ Packet Switching ปกติ
		- MAC (Media Access Control) ควบคุมการเข้าใช้สายหรือสื่อกลาง ทำไมต้องควบคุม? << เพื่อป้องกันการชนกันของข้อมูล
			- MAC 
			- Ethernet
				- ใช้ CSMA ( เช็คว่ามีคนอื่นส่งอยู่มั้ย เพื่อป้องกันการชนกัน ซึ่งจะกะจังหวะกันเองว่าส่งตอนไหน )
			- Wi-Fi
				- ใช้ CSMA , CA ( Collision avoidance ) 
			- STP , VLAN , LACP