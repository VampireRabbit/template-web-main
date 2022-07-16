<script setup>
const state = ['Now it turns to the blue player', 'The red player wins!', 'Now it turns to the red player', 'The blue player wins!', 'Game ends with a draw.']
let board = $ref([])
let cho = $ref(1)
for(let i = 0; i < 10; i++) board.push(0)
function act (i) {
  if (checkwin(board)) return
  if (board[i]) return
  if (board[i] === 0) board[i] = cho
  cho = -1 * cho
}
function gridcolor (i) {
  if (board[i] === 1) return 'bg-red-400'
  if (board[i] === 0) return 'bg-white'
  if (board[i] === -1) return 'bg-blue-500'
}
function checkwin (arr) {
  if (Math.abs(arr[1] + arr[5] + arr[9]) === 3) return true
  if (Math.abs(arr[3] + arr[5] + arr[7]) === 3) return true
  for (let i = 1; i < 8; i += 3) if (Math.abs(arr[i] + arr[i+1] + arr[i+2]) === 3) return true
  for (let i = 1; i < 4; i++) if (Math.abs(arr[i] + arr[i+3] + arr[i+6]) === 3) return true
  return false
}
function checkend (arr) {
  for (let i = 1; i < 10; i++) {
    if (arr[i] == 0) return false
  }
  return true
}
function restart () {
  cho = 1
  for (let i = 0; i < 10; i++) board[i] = 0
}
</script>

<template> 
  <div class="h-screen w-screen bg-slate-200 flex flex-col justify-around items-center">
    <div class="font-serif text-3xl">Tic-Tac-Toe</div>
    <div v-if="checkwin(board)" class="py-2 px-3 rounded-full bg-white font-bold">
    {{ state[cho + 2] }}
    </div>
    <div v-else-if="checkend(board)" class="py-2 px-3 rounded-full bg-white font-bold">{{ state[4] }}</div>
    <div v-else class="py-2 px-3 rounded-full bg-white">{{ state[cho + 1] }}</div>
    <div class="grid grid-cols-3">
      <div v-for="i in 9" @click="act(i)" class="p-12 border-2 cursor-pointer" :class="gridcolor(i)"></div>
    </div>
    <button @click="restart()" class="py-2 px-6 rounded-full bg-purple-500 text-white all-transition hover:shadow-md">
    Restart
    </button>
  </div>
</template> 

<style scoped>

</style>