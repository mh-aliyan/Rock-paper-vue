<template>
  <div>
    <Scores ref="scoress" @add-new-game="addNewGame()"></Scores>
    <footaa @reset-clicked="resetEveryThing()"></footaa>

    <Game 
      v-for="gameId in numberOfGame" 
      :key="gameId" 
      ref="allGames"
      @result="gameresult"
      >
    </Game>


  </div>
</template>

<script>
import Game from "./Game.vue";
import Scores from "./Scores.vue";
import footaa from "./footaa.vue";

export default {
  data(){
    return{
    numberOfGame :[0],
    }
  },
  components: { Game, Scores, footaa },
  methods: {
    resetEveryThing() {
      this.numberOfGame = [0]
      this.$refs.scoress.reset()
      this.$refs.allGames[0].reset()
    },
    gameresult(result){
      this.$refs.scoress.gameScore(result)
    },
    addNewGame(){

      this.numberOfGame.unshift(this.numberOfGame[0] + 1);
    }
}
};

</script>

