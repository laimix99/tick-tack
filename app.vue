<script setup>
// const state = reactive({
//   player: 'X',
//   squares: [
//     ['', '', ''],
//     ['', '', ''],
//     ['', '', ''],
//   ],
// winner: computed(() => calculateWinner(state.squares.flat()))
// });
const player = ref('X');
const squares = ref([
  ['', '', ''],
  ['', '', ''],
  ['', '', ''],
]);
const winner = computed(() => calculateWinner(squares.value.flat()));

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 5],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}

function move(x, y) {
  if (winner.value) return;
  squares.value[x][y] = player.value;
  player.value = player.value === 'O' ? 'X' : 'O';
}

function reset() {
  player.value = 'X';
  squares.value = [
    ['', '', ''],
    ['', '', ''],
    ['', '', ''],
  ];
}

onMounted(() => {});
</script>

<template>
  <div class="w-full flex flex-col items-center justify-center gap-6">
    <div class="w-full flex flex-col items-center justify-center gap-6">
      <h1 v-if="winner">winner {{ winner }}</h1>
      <h2 v-else>{{ player }}</h2>
      <button @click="reset">reset</button>
    </div>
    <div class="flex flex-col flex-wrap items-center w-full cursor-pointer">
      <div
        v-for="x in 3"
        :key="x"
        class="
          <!--
          cub
          flex flex-row
          justify-center
          items-center
          hover:bg-red
          bb
          -->
        "
      >
        <button
          v-for="y in 3"
          :key="y"
          @click="move(x, y)"
          class="w-50px h-50px"
        >
          {{ squares[x][y] }}
        </button>
      </div>
    </div>
  </div>
</template>

<style>
/* .br {
  outline: 1px solid red;
}
.cub {
}
.cub:nth-child(1) {
  border-right: 2px solid black;
  border-bottom: 2px solid black;
}
.cub:nth-child(4) {
  border-right: 2px solid black;
  border-bottom: 2px solid black;
}
.cub:nth-child(2) {
  border-right: 2px solid black;
  border-bottom: 2px solid black;
}
.cub:nth-child(5) {
  border-right: 2px solid black;
  border-bottom: 2px solid black;
}
.cub:nth-child(7) {
  border-right: 2px solid black;
}
.cub:nth-child(3) {
  border-bottom: 2px solid black;
}
.cub:nth-child(6) {
  border-bottom: 2px solid black;
}
.cub:nth-child(9) {
  border-left: 2px solid black;
}

.cell {
  width: 50px;
  height: 50px;
  background-color: white;
  border: black 1px double;
  cursor: pointer;
  display: inline-block;
  user-select: none;
}

.cell:hover {
  border: 1px double red;
}

.X,
.O {
  font-size: 40px;
} */
</style>
