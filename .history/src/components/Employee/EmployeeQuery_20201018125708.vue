<template>
  <div class="employee">
    <!-- 面包屑导航 -->
    <el-breadcrumb separator="/">
      <el-breadcrumb-item>当前位置：员工管理</el-breadcrumb-item>
      <el-breadcrumb-item><a href="/">员工查询</a></el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 查询输入框 -->
    <el-card>
      <el-row>
        职位：
        <div class="options">
          <el-select
            v-model="userInfo.jobId"
            slot="prepend"
            placeholder="请选择职位"
          >
            <el-option label="管理员" value="1"></el-option>
            <el-option label="普通用户" value="2"></el-option>
          </el-select>
        </div>

        姓名：
        <el-input v-model="userInfo.name"></el-input>
        身份证号码：
        <el-input v-model="userInfo.cardId"></el-input>
      </el-row>
      <el-row>
        性别：
        <div class="options">
          <el-select
            v-model="userInfo.sex"
            slot="prepend"
            placeholder="请选择姓名"
          >
            <el-option label="男" value="1"></el-option>
            <el-option label="女" value="2"></el-option>
          </el-select>
        </div>
        手机：
        <el-input v-model="userInfo.phone"></el-input>
        所属部门：
        <div class="options">
          <el-select
            v-model="userInfo.deptId"
            slot="prepend"
            placeholder="--部门选择--"
          >
            <el-option label="技术部" value="1"></el-option>
            <el-option label="管理部" value="2"></el-option>
          </el-select>
        </div>
        <el-button @click="searchEmpolyee">搜索</el-button>
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
        <el-table-column type="selection" width="50"> </el-table-column>
        <el-table-column prop="name" label="姓名" width="50">
          <template slot-scope="scope">{{ scope.row.name }}</template>
        </el-table-column>
        <el-table-column prop="sex" label="性别" width="50"> </el-table-column>
        <el-table-column prop="phone" label="手机号码" width="120">
        </el-table-column>
        <el-table-column prop="email" label="邮箱" width="120">
        </el-table-column>
        <el-table-column prop="job" label="职位" width="80"> </el-table-column>
        <el-table-column prop="education" label="学历" width="50">
        </el-table-column>
        <el-table-column prop="IdNumber" label="身份证号码" width="120">
        </el-table-column>
        <el-table-column prop="door" label="部门" width="120">
        </el-table-column>
        <el-table-column prop="address" label="联系地址" width="200">
        </el-table-column>
        <el-table-column prop="date" label="建档日期" width="120">
        </el-table-column>
        <el-table-column label="操作" width="50">
          <img src="../../assets/images/update.gif" alt="" @click="update" />
        </el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [],
      multipleSelection: [],
      // 默认用户信息
      userInfo: {
        jobId: "",
        name: "",
        sex: "",
        deptId: "",
        cardId: "",
        phone: "",
      },
    };
  },
  created() {
    this.getEmployee();
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
    async handleSelectionChange(val) {
      console.log(val[0]);
      const { data: res } = await this.$http.post(
        "/api//employee/deleteByCondition",
        {
          name: val[0].id,
        }
      );
      this.getEmployee();
    },
    async getEmployee() {
      const { data: res } = await this.$http.post(
        "/api/employee/queryByCondition",
        {}
      );
      this.tableData = res.queryData.list;
      console.log(this.tableData[i].jobId);
    },
    async searchEmpolyee() {
      const { data: res } = await this.$http.post(
        "/api/employee/queryByCondition",
        this.userInfo
      );
      console.log(res);
      this.tableData = res.queryData.list;
      console.log(this.tableData[i].jobId);
    },
    update() {
      this.$router.push("/updateEmployee");
    },
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
.el-pagination {
  margin: 0 auto;
}
.options {
  display: inline;
}
</style>
