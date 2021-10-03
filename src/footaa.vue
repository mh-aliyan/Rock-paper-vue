<template>
  <div
    class="d-flex flex-row justify-content-center text-center controls shadow rounded"
  >
    <div class="flex-fill">
      <button @click="$emit('reset-clicked')" class="btn btn-warning">
        Reset
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "footaa",
};
</script>

<style></style>
