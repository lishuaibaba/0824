<template>
  <div>
    <el-table
      :data="list"
      style="width: 100%; margin-bottom: 20px"
      row-key="id"
      border
      default-expand-all
      :tree-props="{ children: 'children', hasChildren: 'hasChildren' }"
    >
      <el-table-column prop="id" label="商品编号" sortable width="110">
      </el-table-column>
      <el-table-column prop="goodsname" label="商品名称" sortable width="110">
      </el-table-column>
      <el-table-column prop="price" label="商品价格" sortable width="110">
      </el-table-column>
      <el-table-column prop="market_price" label="市场价格" sortable width="110">
      </el-table-column>
      <el-table-column label="图片" sortable width="110">
        <template slot-scope="scope">
          <img :src="$preImg+scope.row.img" alt="">
        </template>
      </el-table-column>

       <el-table-column prop="status" label="是否新品" width="100">
        <template slot-scope="scope">
          <el-button type="primary" v-if="scope.row.isnew == 1"
            >是</el-button
          >
          <el-button type="danger" v-else>否</el-button>
        </template>
      </el-table-column>

       <el-table-column prop="status" label="是否热卖" width="100">
        <template slot-scope="scope">
          <el-button type="primary" v-if="scope.row.ishot == 1"
            >是</el-button
          >
          <el-button type="danger" v-else>否</el-button>
        </template>
      </el-table-column>

      <el-table-column prop="status" label="状态" width="110">
        <template slot-scope="scope">
          <el-button type="primary" v-if="scope.row.status == 1"
            >启用</el-button
          >
          <el-button type="danger" v-else>禁用</el-button>
        </template>
      </el-table-column>

      <el-table-column prop="address" label="操作" width="190">
        <template slot-scope="scope">
          <el-button type="primary" @click="edit(scope.row.id)">编辑</el-button>
          <el-button type="danger" @click="del(scope.row.id)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
import { mapActions, mapGetters } from "vuex";
import { reqgoodsDel } from "../../../util/request";
export default {
  computed: {
    ...mapGetters({
      list: "goods/list",
    }),
  },
  components: {},
  data() {
    return {};
  },
  methods: {
    edit(id) {
      this.$emit("edit", id);
    },
    del(id) {
      reqgoodsDel({ id: id }).then((res) => {
        alert("删除成功");
        this.requestgoodsList();
      });
    },
    ...mapActions({
      requestgoodsList: "goods/requestgoodsList",
    }),
  },
  mounted() {
    this.requestgoodsList();
  },
};
</script>
<style scoped>

img{
  width: 80px;
  height: 80px;
}
</style>