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
##### การสร้าง Server Block
- ขั้นตอนทั้งหมดข้างล่างนี้ ใช้สิทธิ root ทำเกือบทั้งหมดเลยนะจ๊ะ จุ๊บ ๆ 
- สร้าง dir ไว้ที่ /var/www/{server-name}/html ด้วย `sudo mkdir -p /var/www/<server-name>/html`
- ให้สิทธิ $USER ด้วย เราจะได้ทำอะไรกับมันได้ ด้วย `sudo chown -R $USER: /var/www/<server-name>/html`
- สร้างหน้า index.html ไว้ที่ /html ด้วย
- จากนั้นก็ไปตั้งค่า nginx
- ให้เข้าไปที่ /etc/nginx ก่อนนะจ๊ะ
- สร้าง config ของ server block แนะนำว่าให้ copy default มาเลย ด้วย `sudo cp -v sites-available/default sites-available/<server-name>`
- แล้วก็ nano เข้าไปด้วยเพื่อไปแก้ config
- จากนั้นให้สร้าง symbolic link จาก sites-enableed ไปที่ server ของเรา ด้วย `sudo ln -s /etc/nginx/sites-available/<server-name> sites-enabled/`
- อย่า reload nginx ทันทีนะ ให้ test ก่อนด้วย `sudo nginx -t`
- ถ้ามีปัญหาอะไรให้ไปดูที่ /var/log/nginx/error.log
- ถ้ามีไม่มีปัญหาอะไร ก็ reload ได้ด้วยการส่งสัญญาณให้ service nginx ด้วย `sudo nginx -s reload`
#### Hosting SPA with Vue.js and Vite
