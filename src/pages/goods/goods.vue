<template>
  <div>
    <el-button type="primary" @click="willAdd">添加</el-button>
    <v-add :info="info" ref="one"></v-add>
    <v-list @edit="edit($event)"></v-list>
  </div>
</template>
<script>
import vList from "./components/list";
import vAdd from "./components/add";
export default {
  components: {
    vList,
    vAdd,
  },
  data() {
    return {
      info: {
        isShow: false,
        title: "商品管理添加",
        isAdd: true,
      },
    };
  },
  methods: {
    willAdd() {
      this.info.isShow = !this.info.isShow;
      this.info.title = "商品管理添加";
      this.info.isAdd = true;
      this.$refs.one.empty()
    },
    edit(id) {
      this.info.isShow = true;
      this.$refs.one.look(id);
      this.info.title = "商品管理修改";
      this.info.isAdd = false;
    },
  },
  mounted() {},
};
</script>
<style>
</style>