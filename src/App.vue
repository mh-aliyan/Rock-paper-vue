<template>
  <div>
    <Scores ref="scoress"></Scores>
    <Game ref="game1" @result="gameresult"> </Game>
    <Game ref="game2" @result="gameresult"></Game>
    <Game ref="game3" @result="gameresult"></Game>
    <Game ref="game4" @result="gameresult"></Game>
    <Game ref="game5" @result="gameresult"></Game>
    <footaa @reset-clicked="resetEveryThing()"></footaa>

  </div>
</template>

<script>
import Game from "./Game.vue";
import Scores from "./Scores.vue";
import footaa from "./footaa.vue";

export default {
  components: { Game, Scores, footaa },
  methods: {
    resetEveryThing() {
      this.$refs.game1.reset()
      this.$refs.game2.reset()
      this.$refs.game3.reset()
      this.$refs.game4.reset()
      this.$refs.game5.reset()
      this.$refs.scoress.reset()
    },
    gameresult(result){
      this.$refs.scoress.gameScore(result)
    }
}
};

</script>
