<template>
  <div class="aki-col" :class="colClass" :style="colStyle">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Col extends Vue {
  name = "AkiCol";
  @Prop([Number, String]) span?: number | string;
  @Prop([Number, String]) offset?: number | string;
  _gutter = 0;
  get colClass() {
    let { span, offset } = this;
    return [span && `col-${span}`, offset && `offset-${offset}`];
  }
  get colStyle() {
    return {
      paddingLeft: this._gutter / 2 + "px",
      paddingRight: this._gutter / 2 + "px",
    };
  }
}
</script>

<style lang='scss' scoped>
.aki-col {
  $class-prefix: col-;
  @for $n from 1 through 24 {
    &.#{$class-prefix}#{$n} {
      width: $n / 24 * 100%;
    }
  }

  $class-prefix: offset-;
  @for $n from 1 through 24 {
    &.#{$class-prefix}#{$n} {
      margin-left: $n / 24 * 100%;
    }
  }
}
</style>