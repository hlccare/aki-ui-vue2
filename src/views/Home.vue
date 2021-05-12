<template>
  <div class="home">
    <div class="box">
      <Button :loading="loading1" @click="loading1 = !loading1">按钮</Button>
      <Button :loading="loading2" @click="loading2 = !loading2" icon="setting"
        >按钮</Button
      >
      <Button
        :loading="loading3"
        @click="loading3 = !loading3"
        icon="setting"
        iconPosition="right"
        >按钮</Button
      >
      <Button
        :loading="loading4"
        @click="loading4 = !loading4"
        icon="download"
        iconPosition="left"
        >按钮</Button
      >
    </div>
    <div class="box">
      <button-group>
        <Button icon="left">上一页</Button>
        <Button>首页</Button>
        <Button icon="right" iconPosition="right">下一页</Button>
      </button-group>
    </div>

    <div class="box">
      <Input v-model="message" />
      <Input value="内容2" />
      <Input value="禁用" disabled />
      <Input value="只读" readonly />
      <Input value="错误情况" error="内容不得少于5个字" />
    </div>
    <div class="box">
      <Row>
        <Col>1</Col>
        <Col>2</Col>
      </Row>
      <Row>
        <Col>1</Col>
        <Col>2</Col>
        <Col>3</Col>
      </Row>
      <Row>
        <Col>1</Col>
        <Col>2</Col>
        <Col>3</Col>
        <Col>4</Col>
      </Row>
      <Row>
        <Col span="2">2</Col>
        <Col span="22">22</Col>
      </Row>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Button from "@/components/Button.vue";
import ButtonGroup from "../components/ButtonGroup.vue";
import Input from "../components/Input.vue";
import Row from "../components/Row.vue";
import Col from "../components/Col.vue";

@Component({
  components: { Button, ButtonGroup, Input, Row, Col },
})
export default class Home extends Vue {
  data() {
    return {
      loading1: true,
      loading2: true,
      loading3: false,
      loading4: false,
      message: "初始内容",
    };
  }
}
</script>
<style lang="scss" scoped>
.home {
  padding: 20px;
  > .box {
    padding: 10px;
  }
}
</style>
