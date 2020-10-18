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
		<el-input></el-input>
		公告内容: 
		<el-input></el-input>
        <el-button>搜索</el-button>
        <el-button>删除</el-button>
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
        <el-table-column prop="name" label="公告名称" width="120">
          <template slot-scope="scope">{{ scope.row.name }}</template>
        </el-table-column>
        <el-table-column prop="sex" label="公告内容" width="120"> </el-table-column>
        <el-table-column prop="phone" label="创建时间" width="120">
        </el-table-column>
        <el-table-column prop="sex" label="公告人" width="120"> </el-table-column>
        <el-table-column prop="email" label="操作" width="120">
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
      options: [
        {
          value: "选项1",
          label: "经理",
        },
        {
          value: "选项2",
          label: "职员",
        },
      ],
      optionsSex: [
        {
          value: "选项1",
          label: "男",
        },
        {
          value: "选项2",
          label: "女",
        },
      ],
      optionsDoor: [
        {
          value: "选项1",
          label: "技术部",
        },
        {
          value: "选项2",
          label: "运营部",
        },
      ],
      tableData: [],
      multipleSelection: [],
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
      this.multipleSelection = val;
    },
    async getNotice() {
      const { data: res } = await this.$http.post(
        "/api/notice/queryByCondition",
        {}
      );
      console.log(res)
      this.tableData = res.queryData.list[0];
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
