Learning Outcome
- VLAN
สมมุติว่าเวลาจะแยก network ของแผนก เราจะเอา switch ไปวางแยกเลยก็ได้ แต่เขาจะไม่ทำกัน เพราะ user มีการเปลี่ยนแปลงอยู่เสมอ แต่ Hardware เปลี่ยนแปลงได้ยาก จึงนิยมแบ่งด้วย VLAN แทน เพราะเป็นการแบ่งแบบ Virtual

Broadcast Domain หลังจากเราแบ่ง VLAN จะกลายเป็นว่าเราไปแบ่งการ Broadcast ของมัน สมมุติว่าเวลาติดไวรัสก็ไม่สามารถแพร่ไปที่อื่นได้

Utilization จะดีขึ้น เพราะโอกาส Collision จะลดลง เพราะเราแบ่ง broadcast domain ไว้แล้ว จะเหลือก็แค่การชนกันเองใน domain เดียวกัน

Security เน็ตเวิร์คแยกออกจากกันทำให้ไม่สามารถข้ามไปข้ามมาได้

Data link layer domain
- Broadcast Domain การตีกรอบการ Broadcast
- Collision 