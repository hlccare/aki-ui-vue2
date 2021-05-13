<template>
  <div class="aki-tabs-item">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class TabsItem extends Vue {
  name = "AkiTabsItem";
  @Prop({ type: Boolean, default: false }) disabled!: Boolean;
}
</script>

<style scoped>
</style>