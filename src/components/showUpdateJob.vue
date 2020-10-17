<template>
  <div>
    <!-- 面包屑导航区域 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>职位管理</el-breadcrumb-item>
      <el-breadcrumb-item>职位查询</el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 卡片视图区域 -->
    <el-card class="box-card">
		
      <!-- 添加和搜索 -->
      <el-row :gutter="10">
        <el-col :span="12"
          ><div>
            职位名称：<el-input
              label="职位名称"
              placeholder="请输入内容"
              class="input_job"
            ></el-input>
            </div>
            </el-col>
        <el-col :span="3"
          ><div>
            <el-button slot="append" icon="el-icon-search"></el-button></div
        ></el-col>
        <el-col :span="3"
          ><div>
            <el-button slot="" icon="el-icon-delete"></el-button></div
        ></el-col>
      </el-row>
    </el-card>

    <!-- 职位列表 -->

    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column prop="check" type='selection' width="50px"> </el-table-column>
      <el-table-column prop="jobname" label="职位名称" width="180">
      </el-table-column>
      <el-table-column prop="message" label="详细信息" width="180">
      </el-table-column>
      <el-table-column prop="operate" label="操作"> </el-table-column>
    </el-table>

    <!-- 分页 -->
       <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="userInfo.pagenum"
        :page-sizes="[1, 2, 5, 10]"
        :page-size="userInfo.pagesize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="3"
      >
      </el-pagination>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          check: "",
          jobname: "java",
          message:'技术部',
          operate: "caozuo",
        },
        {
          check: "",
          jobname: "web",
          message:'技术部',
          operate: "caozuo",
        },
        
      ],
      input_job : "",
      userInfo: {
        query: "",
        pagenum: 1,
        pagesize: 2
      },
      
    };
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
    // 监听pagesize的变化
    handleSizeChange(newSize) {
      this.userInfo.pagesize = newSize;
      this.getUserList();
    },
    // 监听页码值的变化
    handleCurrentChange(newPage) {
      this.userInfo.pagenum = newPage;
      this.getUserList();
    }
  },
};
</script>

<style lang='less' scoped>
.el-input{
  width: 400px;
}
</style>
