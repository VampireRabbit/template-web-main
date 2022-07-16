<script setup>
const state = ['Now it turns to the blue player', 'The red player wins!', 'Now it turns to the red player', 'The blue player wins!', 'Game ends with a draw.']
let board = $ref([]), block = $ref(0), cho = $ref(1)
restart()
function act (i, j) {
  if (board[0][0]) return
  if (board[i][j]) return
  if ((!checkEnd(board[block])) && block !== 0 && i !== block) return
  if (board[i][j] === 0) board[i][j] = cho
  cho = -1 * cho
  if (board[0][i] === 0 && checkWin(board[i])) board[0][i] = cho
  if (checkEnd(board[i])) board[i][0] = 1
  let sum = 0
  for (let c = 1; c < 10; c++) {
    if (board[c][0]) sum++
  }
  if (checkWin(board[0]) || sum === 9) board[0][0] = 1
  block = j
}
function gridColor (i, j) {
  if (board[0][i] != 0) return 'opacity-0'
  if (board[i][j] === 1) return 'bg-red-400'
  if (board[i][j] === -1) return 'bg-blue-500'
  if (checkWin(board[0])) return 'bg-gray-300'
  if ((!checkEnd(board[block])) && block && i !== block) return 'bg-gray-300'
  return 'bg-white'
}
function bigColor (i) {
  if (board[0][i] === -1) return 'bg-red-400'
  if (board[0][i] === 1) return 'bg-blue-500'
  return ''
}
function checkWin (arr) {
  if (Math.abs(arr[1] + arr[5] + arr[9]) === 3) return true
  if (Math.abs(arr[3] + arr[5] + arr[7]) === 3) return true
  for (let i = 1; i < 8; i += 3) if (Math.abs(arr[i] + arr[i+1] + arr[i+2]) === 3) return true
  for (let i = 1; i < 4; i++) if (Math.abs(arr[i] + arr[i+3] + arr[i+6]) === 3) return true
  return false
}
function checkEnd (arr) {
  if (checkWin(arr)) return true
  for (let i = 1; i < 10; i++) {
    if (arr[i] === 0) return false
  }
  return true
}
function restart () {
  cho = 1, block = 0
  for (let i = 0; i < 10; i++) {
    board[i] = []
    for (let j = 0; j < 10; j++) board[i][j] = 0
  }
}
</script>

<template> 
  <div class="h-screen w-screen bg-slate-200 flex flex-col justify-around items-center">
    <div class="font-serif text-3xl">Ten</div>
    <div v-if="checkWin(board[0])" class="py-2 px-3 rounded-full bg-white font-bold">{{ state[cho + 2] }}</div>
    <div v-else-if="board[0][0]" class="py-2 px-3 rounded-full bg-white font-bold">{{ state[4] }}</div>
    <div v-else class="py-2 px-3 rounded-full bg-white">{{ state[cho + 1] }}</div>
    <div class="grid grid-cols-3">
      <div v-for="i in 9" class="border-2 grid grid-cols-3" :class="bigColor(i)">
        <div v-for="j in 9" @click="act(i, j)" class="all-transition p-6 cursor-pointer border" :class="gridColor(i, j)"></div>
      </div>
    </div>
    <button @click="restart()" class="py-2 px-6 rounded-full bg-purple-500 text-white all-transition hover:shadow-md">Restart
    </button>
  </div>
</template> 