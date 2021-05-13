<template>
  <div class="aki-tabs-head">
    <slot />
    <slot name="actions" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class TabsHeader extends Vue {
  name = "AkiTabsHeader";
}
</script>

<style scoped>
</style>