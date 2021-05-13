<template>
  <div class="aki-tabs">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Tabs extends Vue {
  name = "AkiTabs";
  @Prop({ type: String, required: true }) selected!: String;
  @Prop({
    type: String,
    default: "horizontal",
    validator(value) {
      return ["horizontal", "vertical"].indexOf(value) >= 0;
    },
  })
  direction!: "horizontal" | "vertical";
}
</script>

<style scoped>
</style>