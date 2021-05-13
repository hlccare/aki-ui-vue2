<template>
  <div class="aki-header">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Header extends Vue {
  name = "AkiHeader";
}
</script>

<style scoped>
.aki-header {
}
</style>