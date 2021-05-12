<template>
  <div class="aki-col" :class="[`col-${span}`]">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Col extends Vue {
  name = "AkiCol";
  @Prop([Number, String]) span?: number | string;
}
</script>

<style lang='scss' scoped>
.aki-col {
  height: 100px;
  background: lightblue;
  width: 50%;
  border: 1px solid red;

  $class-prefix: col-;
  @for $n from 1 through 24 {
    &.#{$class-prefix}#{$n} {
      width: $n / 24 * 100%;
    }
  }
}
</style>