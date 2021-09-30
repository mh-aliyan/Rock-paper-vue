<template>
<div>
    <heada></heada>
    <Game></Game>
    <Game></Game>
    <Game></Game>
    <Game></Game>
    <Game></Game>
    <foot></foot>
</div>    
</template>

<script>
import Game from './Game.vue'
import Scores from './Scores.vue'
import foot from './foot.vue'


export default {

  components: { Game, Scores, foot },

}
</script>
