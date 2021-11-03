<template>
  <div>
    <div class="ToolBar"></div>
    <div class="glass ">
      <rpslsp></rpslsp>
      <rps></rps>
    </div>
  </div>
</template>
<script>
import rpslsp from "./r-p-s-l-sp.vue";
import rps from "./r-p-s.vue";

export default {
  components: { rpslsp, rps },
};
</script>
