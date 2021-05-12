<template>
  <div class="aki-row">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Row extends Vue {}
</script>

<style lang='scss' scoped>
.aki-row {
  display: flex;
}
</style>