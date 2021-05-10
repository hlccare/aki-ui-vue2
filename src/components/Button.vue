<template>
  <button class="aki-button">按钮</button>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Button extends Vue {}
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
  &:hover {
    border-color: $border-color-hover;
  }
  &:active {
    background-color: $button-active-bg;
  }
  &:focus {
    outline: none;
  }
}
</style>