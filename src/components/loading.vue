<template>
      <div class="loader" v-html="svg" :style="size"></div>
</template>

<script>
import * as svgLoading from "@/svg/index.js";
export default {
  name: "vue-loading",
  props: {
    type: {
      type: String
    },
    size: { default: () => ({ width: "40px", height: "40px" }) }
  },
  computed: {
    svg() {
      return svgLoading[this.type];
    }
  }
};
</script>

<style>

</style>


