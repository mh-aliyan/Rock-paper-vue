<template>
  <div
    class="d-flex  justify-content-center  controls shadow rounded "
  > 
      <button ref="resetButton" @click="$emit('reset-clicked'); $refs.resetButton.blur()" class="btn btn-warning">
        Reset
      </button>
  </div>
</template>

<script>
export default {
  name: "footaa",
};
</script>

<style></style>
