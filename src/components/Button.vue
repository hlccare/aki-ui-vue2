<template>
  <button class="aki-button" :class="{[`icon-${iconPosition}`]:true}">
    <svg class="icon" aria-hidden="true" v-if="icon">
      <use :xlink:href="`#icon-${icon}`"></use>
    </svg>
    <span class="content">
    <slot />
    </span>
  </button>
  
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Button extends Vue {
  @Prop() icon?: string;
  @Prop({
    default:'left',
    type: String,
    validator:value=>{
      return value==='left'|| value==='right'
  }}) iconPosition?:'left'|'right';
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
  > .icon{
    order: 1;
    margin-right: .1em;
  }
  >.content{
    order: 2;
  }
  &.icon-right{
    > .icon{
      order:2;
      margin-left: .1em;
    }
    >.content{
      order: 1;
    }
  }
}
</style>