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
    <div class="box" style="border: 1px solid black">
      <Row>
        <Col
          span="24"
          :ipad="{ span: 12 }"
          :narrowPc="{ span: 8 }"
          :pc="{ span: 6 }"
          :widePc="{ span: 4 }"
          >1</Col
        >
        <Col
          span="24"
          :ipad="{ span: 12 }"
          :narrowPc="{ span: 8 }"
          :pc="{ span: 6 }"
          :widePc="{ span: 4 }"
        ></Col>
        <Col
          span="24"
          :ipad="{ span: 12 }"
          :narrowPc="{ span: 8 }"
          :pc="{ span: 6 }"
          :widePc="{ span: 4 }"
        ></Col>
        <Col
          span="24"
          :ipad="{ span: 12 }"
          :narrowPc="{ span: 8 }"
          :pc="{ span: 6 }"
          :widePc="{ span: 4 }"
        ></Col>
        <Col
          span="24"
          :ipad="{ span: 12 }"
          :narrowPc="{ span: 8 }"
          :pc="{ span: 6 }"
          :widePc="{ span: 4 }"
        ></Col>
        <Col
          span="24"
          :ipad="{ span: 12 }"
          :narrowPc="{ span: 8 }"
          :pc="{ span: 6 }"
          :widePc="{ span: 4 }"
        ></Col>
      </Row>
      <Row gutter="20">
        <Col
          span="24"
          :ipad="{ span: 8 }"
          :narrowPc="{ span: 4 }"
          :pc="{ span: 2 }"
          :widePc="{ span: 1 }"
          >1</Col
        >
        <Col
          span="24"
          :ipad="{ span: 16 }"
          :narrowPc="{ span: 20 }"
          :pc="{ span: 22 }"
          :widePc="{ span: 23 }"
          >2</Col
        >
      </Row>
      <Row gutter="20">
        <Col>1</Col>
        <Col>2</Col>
      </Row>
      <Row gutter="20">
        <Col>1</Col>
        <Col>2</Col>
        <Col>3</Col>
        <Col>4</Col>
      </Row>
      <Row gutter="20">
        <Col span="2">1</Col>
        <Col span="20" offset="2">11</Col>
      </Row>
      <Row gutter="20">
        <Col span="4">4</Col>
        <Col span="20">20</Col>
      </Row>
      <Row gutter="20">
        <Col span="4">1</Col>
        <Col span="18" offset="2">11</Col>
      </Row>
      <Row gutter="20">
        <Col span="4">1</Col>
        <Col span="8" offset="2">11</Col>
        <Col span="8" offset="2">11</Col>
      </Row>
      <Row gutter="20">
        <Col span="4">1</Col>
        <Col span="4" offset="6">11</Col>
        <Col span="8" offset="2">11</Col>
      </Row>
    </div>
    <div class="box">
      <Layout>
        <Sider class="demo">sider</Sider>
        <Layout>
          <Header class="demo">header</Header>
          <Content class="demo">content</Content>
          <Footer class="demo">footer</Footer>
        </Layout>
      </Layout>
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
import Layout from "../components/Layout.vue";
import Header from "../components/Header.vue";
import Content from "../components/Content.vue";
import Footer from "../components/Footer.vue";
import Sider from "../components/Sider.vue";

@Component({
  components: {
    Button,
    ButtonGroup,
    Input,
    Row,
    Col,
    Layout,
    Header,
    Content,
    Footer,
    Sider,
  },
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
    .demo {
      min-height: 100px;
      border: 1px solid orange;
    }
  }
}
</style>
