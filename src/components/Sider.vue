<template>
  <transition name="slide">
    <div class="aki-sider" v-if="visible">
      <slot />
      <button @click="hide">close</button>
    </div>
  </transition>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Sider extends Vue {
  name = "AkiSider";
  data() {
    return {
      visible: true,
    };
  }
  hide() {
    this.$data.visible = false;
  }
}
</script>

<style lang='scss' scoped>
.aki-sider {
  position: relative;
  width: 200px;
  > button {
    position: absolute;
    top: 0;
    right: 0;
  }
}
.slide-enter-active,
.slide-leave-active {
  transition: all 0.5s;
}
.slide-enter,
.slide-leave-to {
  margin-left: -200px;
}
</style>let