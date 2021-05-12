<template>
  <div class="aki-row" :style="rowStyle" :class="rowClass">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Row extends Vue {
  name = "AkiRow";
  @Prop([Number, String]) gutter?: number | string;
  @Prop({
    type: String,
    validator(value) {
      return ["left", "right", "center"].includes(value);
    },
  })
  align?: "left" | "right" | "center";
  get rowStyle() {
    let { gutter } = this;
    return (
      gutter && {
        marginLeft: -gutter / 2 + "px",
        marginRight: -gutter / 2 + "px",
      }
    );
  }
  get rowClass() {
    let { align } = this;
    return [align && `align-${align}`];
  }
  mounted() {
    this.$children.forEach((vm) => (vm._gutter = this.gutter));
  }
}
</script>

<style lang='scss' scoped>
.aki-row {
  display: flex;
  &.align-left {
    justify-content: flex-start;
  }
  &.align-right {
    justify-content: flex-end;
  }
  &.align-center {
    justify-content: center;
  }
}
</style>