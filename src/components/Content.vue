<template>
  <div class="aki-content">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Content extends Vue {
  name = "AkiContent";
}
</script>

<style scoped>
.aki-content {
  flex-grow: 1;
}
</style>