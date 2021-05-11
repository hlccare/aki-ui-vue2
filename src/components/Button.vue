<template>
  <button class="aki-button" :class="{ [`icon-${iconPosition}`]: true }">
    <Icon v-if="icon" :name="icon" />
    <span class="content">
      <slot />
    </span>
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import Icon from "@/components/Icon.vue";
@Component({
  components: {
    Icon,
  },
})
export default class Button extends Vue {
  @Prop() icon?: string;
  @Prop({
    default: "left",
    type: String,
    validator: (value) => {
      return value === "left" || value === "right";
    },
  })
  iconPosition?: "left" | "right";
}
</script>

<style lang='scss'>
$color: #333;
$border-color: #999;
$border-color-hover: #666;
$button-height: 32px;
$button-bg: white;
$button-active-bg: #eee;
$button-border-radius: 4px;
.aki-button {
  height: $button-height;
  padding: 0 1em;
  font: inherit;
  border-radius: $button-border-radius;
  border: 1px solid $border-color;
  background: $button-bg;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  vertical-align: middle;
  &:hover {
    border-color: $border-color-hover;
  }
  &:active {
    background-color: $button-active-bg;
  }
  &:focus {
    outline: none;
  }
  > .aki-icon {
    order: 1;
    margin-right: 0.1em;
  }
  > .content {
    order: 2;
  }
  &.icon-right {
    > .aki-icon {
      order: 2;
      margin-left: 0.1em;
    }
    > .content {
      order: 1;
    }
  }
}
</style>