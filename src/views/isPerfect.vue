<script setup>
let content = $ref(0)

function isPerfect (x) {
  let res = 1
  for (let i = 2; i<=x/2; i++) {
    if (x % i === 0) res += i
  }
  if (res === x) return true
  else return false
}

</script>

<template>
  <p>Input an Integar to see if it is a Perfect number</p>
  <input type="number" v-model="content">
  <p v-if= "Number.isInteger(content) && content > 1">
    <p v-if="isPerfect(content)">
    Your input: {{ content }} is a Perfect number.
    </p>
    <p v-else>
    Your input: {{ content }} is not a Perfect number.
    </p>
  </p>
  <p v-else>You don't have any valid input</p>
</template>

<style scoped>
input { background-color:lightgray; }
</style>