<template>
  <div>
    <!-- 面包屑导航区域 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>用户管理</el-breadcrumb-item>
      <el-breadcrumb-item>用户查询</el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 卡片视图区域 -->
    <el-card class="box-card">

      <!-- 添加和搜索 -->
      <el-row :gutter="10" >
        <el-col :span="12"
          ><div>
            用户名：<el-input
              label="用户名"
              placeholder="请输入内容"
              v-model="input_user"
              class="input-with-select"
            ></el-input></div
        ></el-col>
        <el-col :span="8"
          ><div>
            用户状态：<el-select
              v-model="select"
              slot="prepend"
              placeholder="全部"
            >
              <el-option label="管理员" value="1"></el-option>
              <el-option label="普通用户" value="2"></el-option>
            </el-select></div
        ></el-col>
        <el-col :span="2"
          ><div>
            <el-button slot="append" icon="el-icon-search" @click="search"></el-button></div
        ></el-col>
        <el-col :span="2"
          ><div>
            <el-button slot="" icon="el-icon-delete"></el-button></div
        ></el-col>
      </el-row>
    </el-card>

    <!-- 用户列表 -->

    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column prop="check" type='selection' width="50px"> </el-table-column>
      <el-table-column prop="loginname" label="登录名" width="180">
      </el-table-column>
      <el-table-column prop="password" label="密码" width="180">
      </el-table-column>
      <el-table-column prop="username" label="用户名"> </el-table-column>
      <el-table-column prop="status" label="状态"> </el-table-column>
      <el-table-column prop="createtime" label="创建时间"> </el-table-column>
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
          loginname: "sonyyq",
          password: "123456",
          username: "王小虎",
          status: "上海市普陀区金沙江路 1518 弄",
          createtime: "2016-05-02",
          operate: "caozuo",
        },
        {
          check: "",
          loginname: "sonyyq",
          password: "123456",
          username: "王小虎",
          status: "上海市普陀区金沙江路 1518 弄",
          createtime: "2016-05-02",
          operate: "caozuo",
        },
        {
          check: "",
          loginname: "sonyyq",
          password: "123456",
          username: "王小虎",
          status: "上海市普陀区金沙江路 1518 弄",
          createtime: "2016-05-02",
          operate: "caozuo",
        },
      ],
      input_user: "",
      select: "",
      // 默认用户信息
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
    },
    search(){
      const res = this.$http.get('/api/user/users?userName=test2')
      console.log(res)
    }
  },
};

</script>

<style  scoped>
.input-with-select .el-input-group__prepend {
  background-color: #fff;
}
.el-input{
  width: 400px;
}
.el-breadcrumb {
  margin: 15px;
}
.el-card {
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.15) !important;
  margin: 15px 0;
}
</style>
