### Client Side II -  vue.js

#### Introduction

#### Basic Command
##### how to create project
```
npm create vue@latest {project-name}
npm install
```
##### how to run project
```
npm run dev
```

#### Github Repository
My git Repo
	[Jhatniphat/INT203-G1 (github.com)](https://github.com/Jhatniphat/INT203-G1)
Professor git Repo
	[GitHub - umaporn-sup/2-2566-Vue-Resources](https://github.com/umaporn-sup/2-2566-Vue-Resources)
#### Sub Topic
[Template Syntax](./Template%20Syntax.md)

ถ้าจะสร้าง variable ที่ให้ access DOM แบบ realtime ให้ใช้ 
```
import {ref} from 'vue'
let count = ref(0)
```
ใน () คือค่าเริ่มต้น
การเข้าถึงและแก้ไขค่านี้ ต้องใช้ .value ด้วย
```
<script setup>
import {ref} from 'vue'
let count = ref(0)
setInterval(()=>{
  count.value = count.value+1
} , 100)
</script>

<template>
  <p>{{ count }}</p>
</template>
```
สามารถใช้ Reactive แทนได้ แต่ใช้ได้แค่ object และไม่ต้อง .value แล้ว