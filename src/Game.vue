<template translate="no" class="py-5">
  <div class="game-instance">
    <div class="cover" v-if="gameIsDone"></div>
    <div class="row">
      <div class="col-md-6 mx-auto">
        <div class="d-flex flex-row justify-content-between align-items-center">
          <div
            class="options d-flex flex-row justify-content-between align-items-center "
          >
            <div
              class="r mr-3"
              :class="yourWeapon == 'Rock' ? 'checked' : ''"
              @click="changeWeapon('Rock')"
            ></div>
            <div
              class="p mr-3"
              :class="yourWeapon == 'Paper' ? 'checked' : ''"
              @click="changeWeapon('Paper')"
            ></div>
            <div
              class="s mr-3"
              :class="yourWeapon == 'Scissor' ? 'checked' : ''"
              @click="changeWeapon('Scissor')"
            ></div>
          </div>
          <div class="game">
            <div class="chooseWeapon " v-if="!yourWeapon">
              Choose your Weapon
            </div>
            <div
              class="fight "
              v-if="yourWeapon && !result"
              v-show="!fighting"
              @click.once="fight"
            >
              FIGHT
            </div>
            <div class="fighting" v-if="fighting">
              <div class="spinner-border text-danger" role="status">
                <span class="sr-only">Loading...</span>
              </div>
            </div>
            <div class="result" :class="result" v-if="result">
              {{ result.toUpperCase() }}
            </div>
          </div>
          <div class="it ml-1">
            <div v-show="computerWeapon === 'Rock'" class="r"></div>
            <div v-show="computerWeapon === 'Paper'" class="p"></div>
            <div v-show="computerWeapon === 'Scissor'" class="s"></div>
          </div>
        </div>

        
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  data() {
    return {
      options: ["Rock", "Paper", "Scissor"],
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
        if (this.yourWeapon === "Scissor") {
          this._lost();
        }
      }
      if (this.computerWeapon === "Paper") {
        if (this.yourWeapon === "Rock") {
          this._lost();
        }
        if (this.yourWeapon === "Scissor") {
          this._win();
        }
      }
      if (this.computerWeapon === "Scissor") {
        if (this.yourWeapon === "Rock") {
          this._win();
        }
        if (this.yourWeapon === "Paper") {
          this._lost();
        }
      }
    },

    changeWeapon(weapon) {
      if (this.fighting) return;
      this.yourWeapon = weapon;
      this.result = "";
      this.computerWeapon = "";
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
      this.result = "draw"
      this.$emit('result','draw')
      
    },

    _win() {
      this.result = "won";
      this.$emit('result','won')
    },

    _lost() {
      this.result = "lost";
      this.$emit('result','lost')
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
