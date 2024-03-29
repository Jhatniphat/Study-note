## **Template Syntax** 

#### {{ content }}
การเขียนนิพจน์ของ js ใน html สามารถใช้ {{ content }} ได้
แนะนำให้เขียนแค่ นิพจน์หรือคำสั่งเดียว ถ้าอยากทำหลาย ๆ คำสั่งให้ไปเขียนฟังก์ชั่นแทน
```
<script setup>
	const getToday=(x)=>{
	  return `Test Calling Function Hi ,${x}`
	}
</script>
<template>
	<h1>{{ getToday() }}</h1>
</template>
```
![Pasted image 20240123105515.png](./Pasted%20image%2020240123105515.png)
#### v-text
Syntax : v-text or {{ content }}
```
<script setup>
	const msg ='<span class="italic"> Hello, World <span>'
</script>
<template>
	<p v-text="msg"></p>
	<p> {{ msg }} </p>
</template>
```

result : element's textContent
![Pasted image 20240123101339.png](./Pasted%20image%2020240123101339.png)

#### v-html
Syntax : v-html
```
<script setup>
	const msg ='<span class="italic"> Hello, World <span>'
</script>
<template>
	<p v-html="msg"></p>
</template>
```
result : element's innerHtml
![Pasted image 20240123100836.png](./Pasted%20image%2020240123100836.png)

#### v-bind
###### Syntax : 
	v-bind
```
<script setup>
	const headingStyle = 'color:Green'
	const isDisibled = true
</script>
<template>
	<h2 :style="headingStyle">Hello , Vue</h2>
    <h2 v-bind:style="headingStyle">Hello , Vue</h2>
    <button class="px-3 py-2 bg-green-600 text-white rounded-xl disabled:bg-slate-500" :disabled="isDisibled">
          Hello World
     </button>
</template>
```
###### result : 
	element's attribute 
เวลาใช้จะต้องบอกด้วยว่าจะใช้เป็นอะไรหลัง : เช่น `v-bind:style`
![Pasted image 20240123102902.png](./Pasted%20image%2020240123102902.png)

#### v-show
Syntax : v-show
```
<script setup>
	const isShow = false;
</script>
<template>
	<h2 v-show="isShow">Hello , Vue</h2>
</template>
```
###### usage : 
	สั่ง show หรือไม่ show ตัว 
	content ไม่ได้หายไปไหน แค่นำ css มาปิดไว้ไม่เหมาะกับข้อมูลที่ sensitive เพราะสามารถเปิด tag ดูได้ มีข้อมูลที่น้ำหนักเบา เหมาะกับงานที่ user เปิดปิดบ่อย
###### result : 
![Pasted image 20240123110248.png](./Pasted%20image%2020240123110248.png)


#### v-if/v-else/v-else-if
Syntax : v-if , v-else , v-else-if
```
<script setup>
	const score = 70
</script>
<template>
	<p v-if="score >= 80">Very Good</p>
    <p v-else-if="score >= 70">Good</p>
    <p v-else>Need Improvement</p>
</template>
```
###### usage : 
	คล้าย v-show แต่จะเข้าไปแก้ไข Dom โดยตรง อันที่ไม่แสดงจะหายไปจาก Dom มีต้นทุนในการเปลี่ยนแปลงค่า
###### result :
![Pasted image 20240123110904.png](./Pasted%20image%2020240123110904.png)

#### v-for
Syntax : v-for
```
<script setup>
	
</script>
<template>
	<div v-for="x in 10">
		<p>{{ x }}</p>
    </div>
</template>
```
##### v-for ( Array and Object )
###### Array
	v-for=" group in groups"
###### Object
	v-for="(course, index) in filterCourses" :key= "course.id"
##### usage : 
	ใช้ในการวนลูปตัว dom ที่เราต้องการ
	ใช้ nested for ได้นะจ๊ะ (ลูปซ้อนลูป...)
###### result :
![Pasted image 20240123111625.png](./Pasted%20image%2020240123111625.png)

#### v-model
Syntax : v-model
```
<script setup>
	import { ref } from 'vue'
	let nickname = ref('')
</script>
<template>
	<input v-model="nickname" placeholder="your nickname">
	<p>Your Nickname is {{ nickname }}</p>
</template>
```
ใช้ในการติดตามค่าของ element นั้น ๆ