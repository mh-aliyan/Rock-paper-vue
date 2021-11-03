<template>
  <div class="game-instance ">
    <div class="cover" v-if="gameIsDone"></div>
    <div class="chose-border ">
      <div class="options">
        <div
          class="r"
          :class="yourWeapon == 'Rock' ? 'checked' : ''"
          @click="changeWeapon('Rock')"
          @dblclick="fight"
          v-if="rock"
        ></div>
        <div
          class="p"
          :class="yourWeapon == 'Paper' ? 'checked' : ''"
          @click="changeWeapon('Paper')"
          @dblclick="fight"
          v-if="paper"
        ></div>
        <div
          class="s"
          :class="yourWeapon == 'Scissor' ? 'checked' : ''"
          @click="changeWeapon('Scissor')"
          @dblclick="fight"
          v-if="scissor"
        ></div>
        <div
          class="l"
          :class="yourWeapon == 'Lizard' ? 'checked' : ''"
          @click="changeWeapon('Lizard')"
          @dblclick="fight"
          v-if="lizard"
        ></div>
        <div
          class="sp"
          :class="yourWeapon == 'Spock' ? 'checked' : ''"
          @click="changeWeapon('Spock')"
          @dblclick="fight"
          v-if="spock"
        ></div>
      </div>
      <div class="game ">
        <div class="chooseWeapon " v-if="!yourWeapon">
          Choose your Weapon
        </div>
        <button
          class="fight "
          v-if="yourWeapon && !result"
          v-show="!fighting"
          @click.once="fight"
          ref="startFight"
        >
          FIGHT
        </button>
        <div class="fighting" v-if="fighting">
          <div class="spinner-border text-danger" role="status">
            <span class="sr-only">Loading...</span>
          </div>
        </div>
        <div class="result" :class="result" v-if="result">
          {{ result.toUpperCase() }}
        </div>
      </div>
      <div class="it">
        <div v-show="computerWeapon === 'Rock'" class="r"></div>
        <div v-show="computerWeapon === 'Paper'" class="p"></div>
        <div v-show="computerWeapon === 'Scissor'" class="s"></div>
        <div v-show="computerWeapon === 'Lizard'" class="l"></div>
        <div v-show="computerWeapon === 'Spock'" class="sp"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  props: {
    rock: { type: Boolean, default: true },
    paper: { type: Boolean, default: true },
    scissor: { type: Boolean, default: true },
    lizard: { type: Boolean, default: true },
    spock: { type: Boolean, default: true },
  },
  data() {
    let options = [];
    if (this.rock === true) {
      options.push("Rock");
    }
    if (this.paper === true) {
      options.push("Paper");
    }
    if (this.scissor === true) {
      options.push("Scissor");
    }
    if (this.lizard === true) {
      options.push("Lizard");
    }
    if (this.spock === true) {
      options.push("Spock");
    }
    return {
      options: options,
      yourWeapon: "",
      computerWeapon: "",
      result: "",
      totalRounds: 0,
      fighting: false,
      gameIsDone: false,
    };
  },
  methods: {
    fight() {
      this.fighting = true;
      this._pretendProcessing();
    },
    _fight() {
      this.computerWeapon = this.options[
        Math.floor(Math.random() * this.options.length)
      ];
      if (this.yourWeapon === this.computerWeapon) this._draw();
      if (this.computerWeapon === "Rock") {
        if (this.yourWeapon === "Paper") {
          this._win();
        }
        if (this.yourWeapon === "Spock") {
          this._win();
        }
        if (this.yourWeapon === "Scissor") {
          this._lost();
        }
        if (this.yourWeapon === "Lizard") {
          this._lost();
        }
      }
      if (this.computerWeapon === "Paper") {
        if (this.yourWeapon === "Rock") {
          this._lost();
        }
        if (this.yourWeapon === "Lizard") {
          this._win();
        }
        if (this.yourWeapon === "Scissor") {
          this._win();
        }
        if (this.yourWeapon === "Spock") {
          this._lost();
        }
      }

      if (this.computerWeapon === "Scissor") {
        if (this.yourWeapon === "Rock") {
          this._win();
        }
        if (this.yourWeapon === "Spock") {
          this._win();
        }
        if (this.yourWeapon === "Paper") {
          this._lost();
        }
        if (this.yourWeapon === "Lizard") {
          this._lost();
        }
      }

      if (this.computerWeapon === "Lizard") {
        if (this.yourWeapon === "Rock") {
          this._win();
        }
        if (this.yourWeapon === "Scissor") {
          this._win();
        }
        if (this.yourWeapon === "Spock") {
          this._lost();
        }
        if (this.yourWeapon === "Paper") {
          this._lost();
        }
      }

      if (this.computerWeapon === "Spock") {
        if (this.yourWeapon === "Lizard") {
          this._win();
        }
        if (this.yourWeapon === "Rock") {
          this._lost();
        }
        if (this.yourWeapon === "Scissor") {
          this._lost();
        }
        if (this.yourWeapon === "Paper") {
          this._win();
        }
      }
    },

    changeWeapon(weapon) {
      if (this.fighting) return;
      this.yourWeapon = weapon;
      this.result = "";
      this.computerWeapon = "";
      let component = this;
      setTimeout(function() {
        component.$refs.startFight.focus();
      }, 100);
    },

    _pretendProcessing() {
      var x = 0;
      var intervalID = setInterval(() => {
        this.computerWeapon = this.options[
          Math.floor(Math.random() * this.options.length)
        ];

        if (++x === 10) {
          window.clearInterval(intervalID);
          this._fight();
          this.fighting = false;
          this.gameIsDone = true;
        }
      }, 100);
    },

    _draw() {
      this.result = "draw";
      this.$emit("result", "draw");
    },

    _win() {
      this.result = "won";
      this.$emit("result", "won");
    },

    _lost() {
      this.result = "lost";
      this.$emit("result", "lost");
    },

    reset() {
      this.result = "";
      this.yourWeapon = "";
      this.computerWeapon = "";
      this.gameIsDone = false;
    },
  },
};
</script>

<style></style>
