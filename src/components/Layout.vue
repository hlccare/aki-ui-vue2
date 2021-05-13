<template>
  <div class="aki-layout" :class="layoutClass">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Row from "./Row.vue";

@Component
export default class Layout extends Vue {
  name = "AkiLayout";
  layoutClass = {
    "has-sider": false,
  };
  mounted() {
    this.$children.forEach((vm) => {
      if (vm.name === "AkiSider") {
        this.layoutClass["has-sider"] = true;
      }
    });
  }
}
</script>

<style lang='scss' scoped>
.aki-layout {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  height: 700px;
  &.has-sider {
    flex-direction: row;
  }
}
</style>