<template>
  <div class="aki-toast" ref="wrapper">
    <div class="message">
      <slot v-if="!enableHtml" />
      <div v-else v-html="$slots.default[0]"></div>
    </div>
    <div class="line" ref="line"></div>
    <span v-if="closeButton" class="close" @click="onClickClose">{{
      closeButton.text
    }}</span>
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
  @Prop({ type: Boolean, default: true }) autoClose!: boolean;
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
  close() {
    this.$el.remove();
    this.$destroy;
  }
  execAutoClose() {
    if (this.autoClose) {
      setTimeout(() => {
        this.close();
      }, this.autoCloseDelay * 1000);
    }
  }
  updateStyles() {
    this.$nextTick(() => {
      console.log((this.$refs.wrapper as any).getBoundingClientRect().height);
      (this.$refs.line as any).style.height = `${
        (this.$refs.wrapper as any).getBoundingClientRect().height
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
.aki-toast {
  display: flex;
  align-items: center;
  font-size: $font-size;
  line-height: 1.8em;
  color: white;
  min-height: $toast-min-height;
  position: fixed;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  background: $toast-bg;
  box-shadow: 0 0 3px 0 rgba(0, 0, 0, 0.5);
  padding: 0 16px;
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