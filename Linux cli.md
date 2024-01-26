การเข้าใช้งาน
	```ssh <user-name>@lvm65012.sit.kmutt.ac.th```
	password : Aumkung777!
ดู ip address
	```ip a```
Autocomplete and Command history
- Use TAB for autocomplete
- Arrow Up / Down to scroll history
- ALT + < to jump to first command
- ALT + > to jump to last command
- CTRL + a to go to beginning of the line
- CTRL + e to go to the end of the line
- CTRL + u to discard from cursor to the beginning
- CTRL + k to discard from cursor to the end
- !! ระบบจะเปลี่ยนเป็นคำสั่งล่าสุดให้ ใช้ร่วมกับคำสั่งอื่นได้เช่น echo !!
bash shell
- เข้าไปด้วยคำสั่ง```bash```
- ทุกครั้งที่รัน bash จะรัน bashrc ด้วย
	- การแก้ bashrc จะยังไม่เห็นความเปลี่ยนแปลงจนกว่าจะเข้า shell ใหม่
	- เพราะจะถูกเรียกตอนเข้าเท่านั้น
- ไม่ใช่ Login shell
- เวลาออกต้องออกด้วย exit ไม่ใช่ logout
ดู process
	```ps -C <application>```
text editor
- ใช้ nano ง่ายกว่า vi
- ![[./Resource/image/Pasted image 20240125093219.png|Pasted image 20240125093219.png]]
การเปลี่ยน password
- ใช้ ```passwd <ชื่อ user>```
- ถ้าไม่ใส่ user จะ default เป็นเรา
- จะเปลี่ยน password ของคนอื่นได้ต้องมีสิทธิ root
การสร้าง user ใหม่
- ใช้ ```sudo useradd <username>```
- มันจะถามหา password  ของ user ที่ใช้คำสั่งนี้
- ไม่ต้องใส่ password ซ้ำ ตลอดในห้านาทีหลังจากใส่ password ครั้งแรก
การใช้สิทธิ์ root
- ใช้ ```sudo <command>```
- ถ้าเป็นคำสั่งดูข้อมูลจะแสดงของ root ทั้งหมด
- ![[./Resource/image/Pasted image 20240125101146.png|Pasted image 20240125101146.png]]
การสลับ user
- ใช้ ```su [option] <username>```
- จะมีการถามหา password ด้วย
- ออกด้วย ```exit```
ดู id ของ user
- ใช้ ```id <username>```
- ถ้าไม่ใส่ username จะเป็นการดูของตัวเอง
- ![[./Resource/image/Pasted image 20240125100709.png|Pasted image 20240125100709.png]]
whoami vs whoami
- whoami จะบอก current user (เราใช้สิทธิ์เป็นใคร)
-  who am i จะบอกข้อมูลการ login
การเปลี่ยนการเป็นเจ้าของไฟล์
-  ใช้ ```chown <username>: <filename>```
-  ถ้าไม่ใช่เจ้าของไฟล์หรือ root จะเปลี่ยนไม่ได้นะจ๊ะ
การดูไฟล์
- ใช้คำสั่ง ```cat``` ดูทั้งไฟล์
- ใช้คำสั่ง ```more``` ดูเป็นหน้า ๆ
- ใช้คำสั่ง ```less``` สามารถใช้การค้นหาได้
- ใช้คำสั่ง ```head``` ดูข้อมูลตอนต้น
- ใช้คำสั่ง ```tail``` ดูข้อมูลตอนท้าย
- ทั้ง head และ tail สามารถใช้ ```-n <จำนวนบรรทัด>``` เพื่อกำหนดข้อมูลที่จะแสดงได้
- ใช้คำสั่ง ```tac``` ดูข้อมูลแบบย้อนกลับ
- สามารถส่งผลลัพธ์ไปยังคำสั่งต่อไปได้ด้วย
	- ```<command-1> | <command-2> | ....```
	- ผลลัพธ์ของ command-1 จะถูกส่งไปหา command-2
-  ค้นหาคำด้วย ```grep <keyword> <file-path>```
การลบไฟล์
- ใช้คำสั่ง ```rm <filename>```
ข้อมูล File ต่าง ๆ
 - /etc/passwd ตอนแรกจะเก็บ password แต่เข้าถึงได้ทุกคนเลยไม่ปลอดภัย เลยเขียนเป็นข้อมูลของ user แต่ละคนแทน เช่น ชื่อ user,group,ตำแหน่งไฟล์ที่เรียกใช้ตอนเข้ามา
 - /etc/shadow เก็บ password ( เข้ารหัส ) มีแต่ root และ กลุ่ม shadow ที่เข้าถึงได้
 การดูข้อมูลของ file
- ```ls -ld <filename>```
- ```file <filename>```
- ```stat <filename>```