#### Package Management
##### ประเภท
-  main – Canonical-supported free and open-source software
-  Universe – Community-maintained free and open-source software (open-source ที่ดูแลด้วย community)
-  Restricted – Proprietary drivers for devices
-  Multiverse – Software restricted by copyright or legal issues
##### apt and apt-get command
- update
	- update ตัว metadata (local) จาก remote repository
	- แต่จะยังไม่ได้ update packages นะจ๊ะ
```
	- apt update
	- apt-get update
```
- upgrade
	- update package ทั้งหมดเป็นเวอร์ชั่นล่าสุด
```
	- apt upgrade
	- apt-get upgrade
```
- search 
	- Search package ตามชื่อของมัน
```
	- apt search <keyword>
	- apt-cache search <keyword>
```
- show
	- show รายละเอียดของ packages
```
	- apt show <keyword>
	- apt-cache show <keyword>
```
- list install
	- list package ที่ install ทั้งหมด
```
	- apt list --installed
```
- install
	- install package ที่กำหนด
```
	- apt install <package-name>
	- apt-get install <package-name>
```
- remove
	- remove package ที่กำหนด
```
	- apt remove <package-name>
	- apt-get remove <package-name>
```
- purge
	- remove package ที่กำหนด รวมถึง config ด้วย
```
	- apt purge <package-name>
	- apt-get purge <package-name>
```
##### Service Manager
###### systemd
- เป็น system และ service manager มีหน้าที่ในการเรียกใช้ service ต่าง ๆ![Pasted image 20240208123744.png](./Pasted%20image%2020240208123744.png)
- เป็น Process ตัวแรกที่ถูกเรียกขึ้นมาเสมอ เพื่อเรียกตัวอื่น ๆ ตามที่ config ไว้
###### systemctl command
- ใช้เพื่อควมคุม service
- `systemctl [option] <service-name>` 
- option
	- status - show status of service
	- start - start service
	- restart - Stop and start the service
	- reload - Reload service configuration
	- stop - Stop the service
	- enable - Enable the service
	- disable - Disable the service
- `reboot` สั่ง reboot ระบบ