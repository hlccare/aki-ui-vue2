<template>
  <div class="wrapper" :class="{ error: error }">
    <input
      :value="value"
      type="text"
      :readonly="readonly"
      :disabled="disabled"
      @change="$emit('change', $event.target.value)"
      @input="$emit('input', $event.target.value)"
      @focus="$emit('focus', $event.target.value)"
      @blur="$emit('blue', $event.target.value)"
    />
    <template v-if="error">
      <Icon iconName="error" class="icon-error" />
      <span class="error-message">{{ error }}</span>
    </template>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import Icon from "@/components/Icon.vue";

@Component({
  components: {
    Icon,
  },
})
export default class Input extends Vue {
  @Prop(String) value?: string;
  @Prop(Boolean) disabled?: boolean;
  @Prop(Boolean) readonly?: boolean;
  @Prop(String) error?: string;
  name = "AkiInput";
}
</script>

<style lang='scss' scoped>
$height: 32px;
$border-color: #999;
$border-color-hover: #666;
$border-radius: 4px;
$font-size: 12px;
$color-error: #f1453d;
.wrapper {
  font-size: $font-size;
  display: inline-flex;
  align-items: center;
  > *:not(:last-child) {
    margin-right: 0.5em;
  }
  > input {
    height: $height;
    border: 1px solid $border-color;
    border-radius: $border-radius;
    padding: 0 8px;
    font-size: inherit;
    $box-shadow-color: rgba(0, 0, 0, 0.5);

    &:hover {
      border-color: $border-color-hover;
    }
    &:focus {
      box-shadow: inset 0 1px 3px $box-shadow-color;
      outline: none;
    }
    &[disabled],
    &[readonly] {
      border-color: #aaa;
      color: #aaa;
      cursor: not-allowed;
    }
  }
  &.error {
    > input {
      border-color: $color-error;
    }
  }
  .icon-error {
    fill: $color-error;
  }
  .error-message {
    color: $color-error;
  }
}
</style>