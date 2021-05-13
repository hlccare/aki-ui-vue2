<template>
  <div class="wrapper" :class="toastClass">
    <div class="aki-toast" ref="toast">
      <div class="message">
        <slot v-if="!enableHtml" />
        <div v-else v-html="$slots.default[0]"></div>
      </div>
      <div class="line" ref="line"></div>
      <span v-if="closeButton" class="close" @click="onClickClose">{{
        closeButton.text
      }}</span>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

type CloseButton = {
  text: string;
  callback: (toast: any) => void;
};

@Component
export default class Toast extends Vue {
  name = "AkiToast";
  @Prop({
    type: [Number, Boolean],
    default: 5,
    validator(value) {
      return value === false || typeof value === "number";
    },
  })
  autoClose!: false | number;
  @Prop({ type: Number, default: 50 }) autoCloseDelay!: number;
  @Prop({
    type: Object,
    default: () => {
      return {
        text: "关闭",
        callback: undefined,
      };
    },
  })
  closeButton!: CloseButton;
  @Prop({ type: Boolean, default: false }) enableHtml!: boolean;
  @Prop({
    type: String,
    default: "top",
    validator(value) {
      return ["top", "bottom", "middle"].indexOf(value) >= 0;
    },
  })
  position!: "top" | "bottom" | "middle";
  get toastClass() {
    let { position } = this;
    return [`position-${position}`];
  }
  close() {
    this.$el.remove();
    this.$emit("beforeClose");
    this.$destroy;
  }
  execAutoClose() {
    if (this.autoClose) {
      setTimeout(() => {
        this.close();
      }, this.autoClose * 1000);
    }
  }
  updateStyles() {
    this.$nextTick(() => {
      (this.$refs.line as any).style.height = `${
        (this.$refs.toast as any).getBoundingClientRect().height
      }px`;
    });
  }
  onClickClose() {
    this.close();
    this.closeButton &&
      typeof this.closeButton.callback === "function" &&
      this.closeButton.callback(this); //this===toast实例
  }
  mounted() {
    this.updateStyles();
    this.execAutoClose();
  }
}
</script>

<style lang='scss' scoped>
$font-size: 14px;
$toast-min-height: 40px;
$toast-bg: rgba(0, 0, 0, 0.75);
$animation-duration: 300ms;
@keyframes slide-up {
  0% {
    opacity: 0;
    transform: translateY(100%);
  }
  100% {
    opacity: 1;
    transform: translateY(0%);
  }
}
@keyframes slide-down {
  0% {
    opacity: 0;
    transform: translateY(-100%);
  }
  100% {
    opacity: 1;
    transform: translateY(0%);
  }
}
@keyframes fade-in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
.wrapper {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  &.position-top {
    top: 0;
    .aki-toast {
      border-top-left-radius: 0;
      border-top-right-radius: 0;
      animation: slide-up $animation-duration;
    }
  }
  &.position-bottom {
    bottom: 0;
    .aki-toast {
      border-bottom-left-radius: 0;
      border-bottom-right-radius: 0;
      animation: slide-up $animation-duration;
    }
  }
  &.position-middle {
    top: 50%;
    transform: translateX(-50%) translateY(-50%);
    animation: fade-in $animation-duration;
  }
}
.aki-toast {
  display: flex;
  align-items: center;
  font-size: $font-size;
  line-height: 1.8em;
  color: white;
  min-height: $toast-min-height;
  background: $toast-bg;
  box-shadow: 0 0 3px 0 rgba(0, 0, 0, 0.5);
  padding: 0 16px;
  border-radius: 4px;
  .message {
    padding: 8px 0;
  }
  .close {
    padding-left: 16px;
    flex-shrink: 0;
  }
  .line {
    height: 100%;
    border-left: 1px solid #666;
    margin-left: 16px;
  }
}
</style>