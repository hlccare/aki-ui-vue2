<template>
  <div class="home">
    <Button>按钮</Button>
    <Button icon="setting">按钮</Button>
    <Button icon="setting" iconPosition="right">按钮</Button>
    <Button icon="download" iconPosition="left">按钮</Button>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Button from "@/components/Button.vue";

@Component({
  components: { Button },
})
export default class Home extends Vue {}
</script>
