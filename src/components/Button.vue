<template>
  <button
    @click="$emit('click')"
    class="aki-button"
    :class="{ [`icon-${iconPosition}`]: true }"
  >
    <Icon v-if="loading" iconName="loading" class="loading" />
    <Icon v-if="icon && !loading" :iconName="icon" />
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
  @Prop({ type: Boolean, default: false })
  loading?: boolean;
  name = "AkiButton";
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
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
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
    order: 2;
    margin-right: 0.1em;
  }
  > .content {
    order: 3;
  }
  &.icon-right {
    > .aki-icon {
      order: 3;
      margin-left: 0.1em;
    }
    > .content {
      order: 2;
    }
  }
  > .loading.aki-icon {
    animation: spin 1s linear infinite;
  }
}
</style>