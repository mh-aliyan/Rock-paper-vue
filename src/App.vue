<template>
  <div>
    <Scores ref="scoress" @add-new-game="addNewGame()"></Scores>
    <footaa @reset-clicked="resetEveryThing()"></footaa>

    <Game 
      :id="`game${gameId}`" 
      v-for="gameId in n" 
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
    n : 1,
    }
  },
  components: { Game, Scores, footaa },
  methods: {
    resetEveryThing() {
      for (let i = 0; i < this.n; i++){
        this.$refs.allGames[i].reset()
        this.n = 1 
      }
      this.$refs.scoress.reset()
    },
    gameresult(result){
      this.$refs.scoress.gameScore(result)
    },
    addNewGame(){
      this.n++
    }
}
};

</script>

