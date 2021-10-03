<template>
  <div class="container">
    <div class="row">
      <div class="col-md-8 mx-auto">
        <div class="d-flex flex-row justify-content-between">
          <div class="title">Rock . Paper . Scissor .</div>
          <div class="d-flex scores flex-row">
            <div
              class="d-flex align-items-center you mr-3 justify-content-between"
            >
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
            <div class="d-flex align-items-center computer">
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
    </div>
  <div>
      {{finalResult}}
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
      finalResult:"",
    };
  },
  methods: {
    gameScore(result) {
      if (result == "won") {
        this.yourScore++;
        if(this.yourScore > 2){
            this.finalResult = "you win"
        }
      } else if (result == "lost") {
        this.computerScore++;
         if(this.computerScore > 2){
            this.finalResult = "you Lose"
        }
      }

    },
    reset() {
      this.yourScore = 0;
      this.computerScore = 0;
    },
  },
};
</script>

<style></style>
