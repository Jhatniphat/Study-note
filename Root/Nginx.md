#### Command
##### curl 
- transfer a url
-  ```curl <url>```
##### ufw
- ใช้ควบคุม Firewall ของ VM
- `ufw allow '<service-name>'` เพื่อเป็นการ add role ให้ service ผ่านได้
- `ufw deny '<service-name>'` เพื่อเป็นการ add role ให้ service ผ่านไม่ได้
- `ufw delete allow '<service-name> or <role-num>'` เพื่อเป็นการ delete role ให้ service ผ่านไม่ได้
- สามารถดู role num ได้จาก `ufw status numbered`
- ถ้า delete ผ่าน role num แนะนำให้ทำที่เลขเยอะ ๆ ไปเลขน้อย
- `ufw show listening` เป็นการดูว่ามี service อะไรบ้างที่รอรับ request อยู่