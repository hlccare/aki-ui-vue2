<template>
  <div class="aki-tabs-body">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class TabsBody extends Vue {}
</script>

<style scoped>
</style>