<script setup>
let content = $ref(''), list = $ref([])
function swaplist (a,b) { 
  if (a >= 0 && b < list.length) {
    let tmp = list[a]
    list[a] = list[b], list[b] = tmp
  } 
}
</script>

<template>
  <p v-if="content">Your input: {{ content }}</p>
  <p v-else>You don't have any input</p>
  <input v-model="content">
  <button @click="list.push(content)">Add</button>
  <p v-for="(item,i) in list">
    {{ item }}&nbsp;&nbsp;
    <button class="red" @click="list.splice(i, 1)">Remove</button>&nbsp;
    <button class="blue" @click="swaplist(i-1,i)">Moveup</button>&nbsp;
    <button class="blue" @click="swaplist(i,i+1)">Movedown</button>&nbsp;
  </p>
</template>

<style scoped>
input { background-color:lightgray; }
.red { color:crimson; }
.blue { color:blue; }
</style>