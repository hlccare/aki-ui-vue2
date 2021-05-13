<template>
  <div class="aki-col" :class="colClass" :style="colStyle">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

let validator = (value: object): boolean => {
  let keys = Object.keys(value);
  let valid = true;
  keys.forEach((key) => {
    if (["span", "offset"].indexOf(key) < 0) {
      valid = false;
    }
  });
  return valid;
};

interface mediaObject extends Object {
  span?: number | string;
  offset?: number | string;
}

@Component
export default class Col extends Vue {
  name = "AkiCol";
  @Prop([Number, String]) span?: number | string;
  @Prop([Number, String]) offset?: number | string;
  @Prop({ type: Object, validator }) ipad?: mediaObject;
  @Prop({ type: Object, validator }) narrowPc!: mediaObject;
  @Prop({ type: Object, validator }) pc!: mediaObject;
  @Prop({ type: Object, validator }) widePc!: mediaObject;

  colGutter = 0;

  createClasses = (obj: mediaObject | undefined, str = ""): string[] | void => {
    if (!obj) {
      return;
    }
    let array = [];
    if (obj.span) {
      array.push(`col-${str}${obj.span}`);
    }
    if (obj.offset) {
      array.push(`offset-${str}${obj.offset}`);
    }
    return array;
  };

  get colClass() {
    let { span, offset, ipad, narrowPc, pc, widePc } = this;
    let createClasses = this.createClasses;
    return [
      ...(createClasses({ span, offset }) || []),
      ...(createClasses(ipad, "ipad-") || []),
      ...(createClasses(narrowPc, "narrow-pc-") || []),
      ...(createClasses(pc, "pc-") || []),
      ...(createClasses(widePc, "wide-pc-") || []),
      // span && `col-${span}`,
      // offset && `offset-${offset}`,
      // ipad && [`col-ipad-${ipad.span}`],
      // narrowPc && [`col-narrow-pc-${narrowPc.span}`],
      // pc && [`col-pc-${pc.span}`],
      // widePc && [`col-wide-pc-${widePc.span}`],
    ];
  }
  get colStyle() {
    return {
      paddingLeft: this.colGutter / 2 + "px",
      paddingRight: this.colGutter / 2 + "px",
    };
  }
}
</script>

<style lang='scss' scoped>
.aki-col {
  min-height: 30px;
  border: 1px solid blue;
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
  @media (min-width: 577px) {
    $class-prefix: col-ipad-;
    @for $n from 1 through 24 {
      &.#{$class-prefix}#{$n} {
        width: $n / 24 * 100%;
      }
    }

    $class-prefix: offset-ipad-;
    @for $n from 1 through 24 {
      &.#{$class-prefix}#{$n} {
        margin-left: $n / 24 * 100%;
      }
    }
  }
  @media (min-width: 769px) {
    $class-prefix: col-narrow-pc-;
    @for $n from 1 through 24 {
      &.#{$class-prefix}#{$n} {
        width: $n / 24 * 100%;
      }
    }

    $class-prefix: offset-narrow-pc-;
    @for $n from 1 through 24 {
      &.#{$class-prefix}#{$n} {
        margin-left: $n / 24 * 100%;
      }
    }
  }
  @media (min-width: 993px) {
    $class-prefix: col-pc-;
    @for $n from 1 through 24 {
      &.#{$class-prefix}#{$n} {
        width: $n / 24 * 100%;
      }
    }

    $class-prefix: offset-pc-;
    @for $n from 1 through 24 {
      &.#{$class-prefix}#{$n} {
        margin-left: $n / 24 * 100%;
      }
    }
  }
  @media (min-width: 1200px) {
    $class-prefix: col-wide-pc-;
    @for $n from 1 through 24 {
      &.#{$class-prefix}#{$n} {
        width: $n / 24 * 100%;
      }
    }

    $class-prefix: offset-wide-pc-;
    @for $n from 1 through 24 {
      &.#{$class-prefix}#{$n} {
        margin-left: $n / 24 * 100%;
      }
    }
  }
}
</style>