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
import heada from './heada.vue'
import foot from './foot.vue'


export default {

  components: { Game, heada, foot },

}
</script>
