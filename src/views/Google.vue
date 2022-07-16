<script setup>
let a = $ref(0), b = $ref(0), c = $ref(0), d = $ref(0)
</script>

<template>
  <div class="box">
    <div class="box1">
      <img src="Google.svg" class="py-2 pl-1" width="30" height="40">
      <div class="m-1 p-2">Google Docs</div>
      <button @click="a = 1; b = 0; c = 0; d = 0" class="m-1 p-2" :class="a ? 'font-bold underline decoration-blue-500 underline-offset-8' : ''">概览</button>
      <button @click="a = 0; b = 1; c = 0; d = 0" class="m-1 p-2" :class="b ? 'font-bold underline decoration-blue-500 underline-offset-8' : ''">功能</button>
      <button @click="a = 0; b = 0; c = 1; d = 0" class="m-1 p-2" :class="c ? 'font-bold underline decoration-blue-500 underline-offset-8' : ''">安全性</button>
      <button @click="a = 0; b = 0; c = 0; d = 1" class="m-1 p-2" :class="d ? 'font-bold underline decoration-blue-500 underline-offset-8' : ''">定价</button>
    </div>
    <div class="box2">
      <button class="m-1 p-2">更多工具</button>
      <button class="m-1 p-2 text-sky-500">登录</button>
      <button class="mx-1 my-2 px-2 py-1 text-sky-500 rounded border border-slate-300">
        开始使用Google文档
      </button>
      <button class="mx-1 my-2 px-2 py-1 text-white bg-sky-500 rounded border border-sky-500">
        尝试使用Google文档进行办公
      </button>
    </div>
  </div>
</template>

<style scoped>
.box { 
  display: flex; 
  justify-content: space-between;
}
.box1 {
  display: flex;
}
.box2 {
  display: flex;
  justify-content: right;
}
</style>