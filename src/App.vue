<template>
  <div id="app">
    <div class="w-full h-screen flex flex-col items-center">
      <div
        class="border shadow-2xl grid grid-cols-3 w-3/4 lg:w-1/2"
        :style="{ 'background-color': 'rgb(255 251 248)' }"
      >
        <Cell
          v-for="(value, key) in values"
          v-bind:key="key"
          :value="value"
          :index="key"
          :play="() => play(key)"
        >
        </Cell>
        <audio id="audioCat" className="clip" src="./assets/mew.mp3"></audio>
        <audio
          id="audioFish"
          className="clip"
          src="./assets/bubble.mp3"
        ></audio>
      </div>
      <div>
        <Button :onClick="() => reset()">
          Restart <i class="fas fa-redo-alt"></i
        ></Button>
        <Button :onClick="() => undo()">
          Undo <i class="fas fa-undo-alt"></i
        ></Button>
        <Button :onClick="() => autoPlay()">
          Auto play <i class="fas fa-play"></i
        ></Button>
        <Button :onClick="() => playMachine()">
          Play with <i class="fas fa-laptop"></i
        ></Button>
      </div>
      <BannerWin :win="win"> </BannerWin>
    </div>
  </div>
</template>

<script>
import BannerWin from "./components/BannerWin.vue";
import Cell from "./components/Cell.vue";
import Button from "./components/Button.vue";

export default {
  name: "App",
  components: {
    BannerWin,
    Cell,
    Button,
  },
  data: () => ({
    values: {
      1: "",
      2: "",
      3: "",
      4: "",
      5: "",
      6: "",
      7: "",
      8: "",
      9: "",
    },
    current: "X",
    win: "",
    history: [],
    moves: 0,
  }),
  methods: {
    play(key) {
      if (!this.win && !this.values[key]) {
        this.history.push({
          values: { ...this.values },
          current: this.current,
        });
        this.values[key] = this.current;
        this.current = this.current === "X" ? "O" : "X";

        if (this.current === "O") {
          const audio = document.getElementById("audioCat");
          audio.play();
        } else {
          const audio = document.getElementById("audioFish");
          audio.play();
        }
        this.moves++;
      }
      this.calculateWinner();
    },
    reset() {
      this.values = {
        1: "",
        2: "",
        3: "",
        4: "",
        5: "",
        6: "",
        7: "",
        8: "",
        9: "",
      };
      this.current = "X";
      this.win = "";
      this.moves = 0;
    },
    calculateWinner() {
      const horizontalWinner = () => {
        for (let i of [1, 4, 7]) {
          if (
            this.values[i] &&
            this.values[i] === this.values[i + 1] &&
            this.values[i] == this.values[i + 2]
          ) {
            return this.values[i];
          }
        }
        return false;
      };
      const verticalWinner = () => {
        for (let i of [1, 2, 3]) {
          if (
            this.values[i] &&
            this.values[i] === this.values[i + 3] &&
            this.values[i] === this.values[i + 6]
          ) {
            return this.values[i];
          }
        }
        return false;
      };
      const diagWinner = () => {
        if (
          this.values[1] &&
          this.values[1] === this.values[5] &&
          this.values[1] === this.values[9]
        ) {
          return this.values[1];
        }
        if (
          this.values[3] &&
          this.values[3] === this.values[5] &&
          this.values[3] === this.values[7]
        ) {
          return this.values[3];
        }
        return false;
      };
      const winner = horizontalWinner() || verticalWinner() || diagWinner();
      if (winner) {
        this.win = winner;
      } else if (this.moves === 9) {
        this.win = "Empate";
      }
    },
    undo() {
      if (this.win) {
        return;
      }
      if (this.history.length) {
        const { current, values } = this.history.pop();
        this.values = values;
        this.current = current;
        this.moves--;
      }
    },
    autoPlay() {
      if (this.win) {
        return;
      }
      let randomNum = Math.floor(Math.random() * 9 + 1);
      if (this.values[randomNum] === "") {
        this.play(randomNum);
      } else {
        this.autoPlay();
      }
    },
    playMachine() {
      this.reset();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
