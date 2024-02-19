###### State ของ Process
- ![Pasted image 20240201120757.png](./Pasted%20image%2020240201120757.png)
แต่ละ Process จะมี PID (Process ID)
Process Creation
- มีโครงสร้างเป็น Tree![Pasted image 20240201121052.png](./Pasted%20image%2020240201121052.png)
- Parent Process จะเป็นคนสร้าง Children Process
- ตอนที่รันคำสั่ง มันจะสร้าง Process ใหม่ขึ้นมา แล้วโหลดตอนโค้ดของคำสั่งเข้า Process![Pasted image 20240201121338.png](./Pasted%20image%2020240201121338.png)
- ในตัวอย่างคือการรันคำสั่ง ps ซึ่งตัว Bash จะรอให้ทำ ps ให้เสร็จก่อน (Bash หลับรอ )แล้วค่อยทำ Bash ต่อ
###### ==PS== command
- `\_` แสดงถึงความเป็น child process ![Pasted image 20240201122345.png](./Pasted%20image%2020240201122345.png) 
- เวลาเราสร้าง script ไฟล์แล้วเรียกใช้ จะมีการสร้าง shell ขึ้นมาเพื่อรันคำสั่ง![Pasted image 20240201122936.png](./Pasted%20image%2020240201122936.png) 
- ถ้าไม่อยากให้สร้าง shell เพื่อมาใช้คำสั่งใน Script ให้ใช้ source นำหน้า![Pasted image 20240201123222.png](./Pasted%20image%2020240201123222.png)
- **วิธีการอ่านรหัสที่มันแสดงออกมา**![Pasted image 20240201123327.png](./Pasted%20image%2020240201123327.png)
- **ออปชั่นของ ps**![Pasted image 20240208092950.png](./Pasted%20image%2020240208092950.png)
###### การดู pid ของ process นั้น ๆ 
- ใช้ `pidof <process>`
- ใช้ `pgrep <bash>`![Pasted image 20240208094449.png](./Pasted%20image%2020240208094449.png)
###### คำสั่ง Top
- เป็นการดู Top ของการใช้งาน Cpu
- แสดงผลแบบ Realtime![Pasted image 20240208095142.png](./Pasted%20image%2020240208095142.png)
- Task
	- running - process ที่ทำงานอยู่
	- sleep - หลับอยู่ รอการทำงาน
	- stopped - หยุดอยู่
	- zombie - process ที่ตายไปแล้ว แต่ยังคงค้างอยู่ในระบบ
###### การดึง Process ที่ Stop อยู่ให้กลับมาทำงาน
- สั่ง Stop ด้วย CTRL+Z
- ดู process ได้ที่ job
- ใช้คำสั่ง fg เพื่อดึงให้กลับมาทำงานที่ foreground
- ใช้คำสั่ง bg เพื่อดึงให้กลับมาทำงานที่ background
- ทั้งสองคำสั่งจะดึงตัวล่าสุดมาทำ ถ้าต้องการให้ดึงตัวอื่นให้ใส่ `%<ให้ถอยหลังไปเท่าไหร่>`
- ใน lab จะใช้คำสั่ง `sleep <time>`
###### การ kill Process
- ใช้ `kill -<signal num>`
- สามารถใช้ -l เช็คได้ว่าเลขไหนส่ง signal อะไร
- Common Signal
	- SIGTERM (15) ขอให้ Process หยุด ซึ่งขึ้นอยู่กับ Dev ว่าเมื่อได้