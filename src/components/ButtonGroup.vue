<template>
  <div class="aki-button-group">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class ButtonGroup extends Vue {
  name = "AkiButtonGroup";
  mounted() {
    for (let node of this.$el.children) {
      let name = node.nodeName.toLowerCase();
      if (name !== "button") {
        console.warn(`ButtonGroup的子元素应该全是Button,不应该是${name}`);
      }
    }
  }
}
</script>

<style lang='scss' scoped>
.aki-button-group {
  display: inline-flex;
  vertical-align: middle;
  > .aki-button {
    border-radius: 0;
    &:not(:first-child) {
      margin-left: -1px;
    }
    &:first-child {
      border-top-left-radius: 3px;
      border-bottom-left-radius: 3px;
    }
    &:last-child {
      border-top-right-radius: 3px;
      border-bottom-right-radius: 3px;
    }
    &:hover {
      position: relative;
      z-index: 1;
    }
  }
}
</style>