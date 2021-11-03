<template>
  <div>
    <div>
      <div class="d-flex flex-row justify-content-between">
        <div class="title">Rock . Paper . Scissor .</div>

        <div class="d-flex  flex-row score total-score ">
          <div class="you">
            <span class="text">You</span
            ><span
              class="score font-weight-bold"
              :class="
                yourScore >= computerScore ? 'text-success' : 'text-danger'
              "
            >
              {{ yourScore }}</span
            >
          </div>

          <div class="computer">
            <span class="text">Computer</span
            ><span
              class="score font-weight-bold"
              :class="
                computerScore >= yourScore ? 'text-success' : 'text-danger'
              "
            >
              {{ computerScore }}</span
            >
          </div>
        </div>
      </div>
    </div>
    <div :class="resultClasses">
      {{ gameState }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Scores",
  data: function() {
    return {
      yourScore: 0,
      computerScore: 0,
      state: 0,
    };
  },
  computed: {
    gameState() {
      switch (this.state) {
        case 1:
          return "<<you win>>";
        case 2:
          return "<<you lose>>";
        default:
          return "";
      }
    },
    resultClasses() {
      return {
        finalResult: true,
        win: this.state == 1,
        lose: this.state == 2,
      };
    },
  },
  methods: {
    gameScore(result) {
      switch (result) {
        case "won":
          this.yourScore++;
          if (this.yourScore > 2) {
            this.state = 1;
            return;
          }
          break;
        case "lost":
          this.computerScore++;
          if (this.computerScore > 2) {
            this.state = 2;
            return;
          }
          break;
      }
      this.$emit("add-new-game");
    },

    reset() {
      this.yourScore = 0;
      this.computerScore = 0;
      this.state = 0;
    },
  },
};
</script>

<style></style>
