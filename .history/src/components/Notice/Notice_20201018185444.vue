<template>
  <div class="employee">
    <!-- 面包屑导航 -->
    <el-breadcrumb separator="/">
      <el-breadcrumb-item>当前位置：公告管理</el-breadcrumb-item>
      <el-breadcrumb-item><a href="/">公告查询</a></el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 查询输入框 -->
    <el-card>
      <el-row>
        公告名称：
        <el-input v-model="notice.title"></el-input>
        公告内容:
        <el-input v-model="notice.content"></el-input>
        <el-button @click="searchNotice()">搜索</el-button>
        <el-button @click="deleteNotice">删除</el-button>
      </el-row>
    </el-card>
    <!-- Table表格 -->
    <el-card>
      <el-table
        ref="multipleTable"
        :data="tableData"
        tooltip-effect="dark"
        style="width: 100%"
        @selection-change="handleSelectionChange"
      >
        <el-table-column type="selection" width="55"> </el-table-column>
        <el-table-column prop="title" label="公告名称" width="120">
        </el-table-column>
        <el-table-column prop="content" label="公告内容" width="120">
        </el-table-column>
        <el-table-column prop="createDate" label="创建时间" width="120">
        </el-table-column>
        <el-table-column prop="" label="公告人" width="120"> </el-table-column>
        <el-table-column prop="email" label="操作" width="120">
           <img
              src="../../assets/images/update.gif"
              alt=""
            />
        </el-table-column>
        <el-table-column prop="job" label="预览" width="120"> </el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      //公告查询数据
      notice: {
        title: "",
        content: "",
      },
      tableData: [],
      multipleSelection: [],
      title: ""
    };
  },
  created() {
    this.getNotice();
  },
  methods: {
    toggleSelection(rows) {
      if (rows) {
        rows.forEach((row) => {
          this.$refs.multipleTable.toggleRowSelection(row);
        });
      } else {
        this.$refs.multipleTable.clearSelection();
      }
    },
    handleSelectionChange(val) {
      this.title = val[0].title;
      this.multipleSelection = val;
    },
    async getNotice() {
      const { data: res } = await this.$http.post(
        "/api/notice/queryByCondition",
        {}
      );
      this.tableData = res.queryData.list;
    },
    //搜索公告
    async searchNotice() {
      const { data: res } = await this.$http.post(
        "/api/notice/queryByCondition",
       this.notice
      );
      console.log(res);
      this.tableData = res.queryData.list;
    },
    // 删除公告
    async deleteNotice(){
      console.log(this.id)
    const { data: res } = await this.$http.post(
        "/api/notice/deleteByCondition",
        {
          "title": this.title
        }
      );
      console.log(res);
      this.getNotice();
    }
  },
};
</script>

<style lang="less" scoped>
.el-card {
  margin-top: 20px;
}
.el-input {
  width: 250px;
}
.el-row {
  margin-top: 10px;
}
.el-button {
  margin-left: 10px;
}
</style>
