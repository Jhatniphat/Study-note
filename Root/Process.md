State ของ Process
- ![Pasted image 20240201120757](./Pasted%20image%2020240201120757.png)
แต่ละ Process จะมี PID (Process ID)
Process Creation
- มีโครงสร้างเป็น Tree![Pasted image 20240201121052](./Pasted%20image%2020240201121052.png)
- Parent Process จะเป็นคนสร้าง Children Process
- ตอนที่รันคำสั่ง มันจะสร้าง Process ใหม่ขึ้นมา แล้วโหลดตอนโค้ดของคำสั่งเข้า Process![Pasted image 20240201121338](./Pasted%20image%2020240201121338.png)
- ในตัวอย่างคือการรันคำสั่ง ps ซึ่งตัว Bash จะรอให้ทำ ps ให้เสร็จก่อน (Bash หลับรอ )แล้วค่อยทำ Bash ต่อ
- เช็คได้ด้วย ps
- `\_` แสดงถึงความเป็น child process ![Pasted image 20240201122345](./Pasted%20image%2020240201122345.png) 
- เวลาเราสร้าง script ไฟล์แล้วเรียกใช้ จะมีการสร้าง shell ขึ้นมาเพื่อรันคำสั่ง![Pasted image 20240201122936](./Pasted%20image%2020240201122936.png) 
- ถ้าไม่อยากให้สร้าง shell เพื่อมาใช้คำสั่งใน Script ให้ใช้ source นำหน้า![Pasted image 20240201123222](./Pasted%20image%2020240201123222.png)
- วิธีการอ่านรหัสที่มันแสดงออกมา![Pasted image 20240201123327](./Pasted%20image%2020240201123327.png)
- 