<template>
  <div class="aki-footer">
    <slot />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Footer extends Vue {
  name = "AkiFooter";
}
</script>

<style scoped>
.aki-footer {
}
</style>