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
            placeholder="请选择性别"
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
        <el-button @click="deleteEmployee">删除</el-button>
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
          <template slot-scope="scope">
             <img src="../../assets/images/update.gif" alt="" @click="update(scope.row)" />
          </template>
         
        </el-table-column>
      </el-table>
    </el-card>
 
 <el-dialog
  title="更新员工"
  :visible.sync="empolyeeDialogVisible"
  width="70%"
   @close="setRightDialogClosed">
      <el-form
        :model="addForm"
        :rules="addFormRules"
        ref="updateFormRef"
        :inline="true"
      >
        <el-row>
          <el-col :span="8">
            <el-form-item label="姓名" prop="name">
              <el-input v-model="updateUser[0].name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="身份证号码" prop="cardId">
              <el-input v-model="updateUser[0].cardId"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
    <!-- 选择框 -->
	<el-row>
		<el-col :span="8">
           性别：
	   <div class="options">
          <el-select
            v-model="userInfo.sex"
            slot="prepend"
            placeholder="请选择性别"
          >
            <el-option label="男" value="1"></el-option>
            <el-option label="女" value="2"></el-option>
          </el-select>
        </div>
		</el-col>
		<el-col :span="8">
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
		</el-col>
	</el-row>
	

        <el-row>
          <el-col :span="8">
            <el-form-item label="学历" prop="education">
              <el-input v-model="updateUser[0].education"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="邮箱" prop="email">
              <el-input v-model="updateUser[0].email"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

		<el-row>
          <el-col :span="8">
            <el-form-item label="手机" prop="phone">
              <el-input v-model="updateUser[0].phone"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="电话" prop="tel">
              <el-input v-model="updateUser[0].tel"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

   <el-row>
          <el-col :span="8">
            <el-form-item label="政治面貌" prop="name">
              <el-input v-model="updateUser[0].name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="QQ号码" prop="IdNumber">
              <el-input v-model="addForm.IdNumber"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
		<el-row>
          <el-col :span="8">
            <el-form-item label="联系地址" prop="name">
              <el-input v-model="addForm.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="邮政编码" prop="IdNumber">
              <el-input v-model="addForm.IdNumber"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

		<el-row>
          <el-col :span="8">
            <el-form-item label="出生日期" prop="name">
              <el-input v-model="addForm.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="名族" prop="IdNumber">
              <el-input v-model="addForm.IdNumber"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

		<el-row>
          <el-col :span="8">
            <el-form-item label="所学专业" prop="name">
              <el-input v-model="addForm.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="爱好" prop="IdNumber">
              <el-input v-model="addForm.IdNumber"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

		<el-row>
          <el-col :span="8">
            <el-form-item label="备注" prop="name">
              <el-input v-model="addForm.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
			  所属部门：
            <div class="options">
          <el-select
            v-model="userInfo.deptId"
            slot="prepend"
            placeholder="选择部门"
          >
            <el-option label="技术部" value="1"></el-option>
            <el-option label="管理部" value="2"></el-option>
          </el-select>
        </div>
          </el-col>
        </el-row>
        <el-row>
		</el-row>
      </el-form>
  <span slot="footer" class="dialog-footer">
    <el-button @click="empolyeeDialogVisible">取 消</el-button>
    <el-button type="primary" @click="empolyeeDialogVisible">更新</el-button>
  </span>
</el-dialog>
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
       //权限分配对话框的显示与否
      empolyeeDialogVisible: false,
       // 添加表单对象
      addForm: {
        name: "",
        IdNumber: "",
      },
      // 添加表单校验规则对象
     addFormRules: {
        name: [
          { required: true, message: "请输入活动名称", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 3 到 5 个字符", trigger: "blur" },
        ],
        IdNumber: [
          { required: true, message: "请输入活动名称", trigger: "blur" },
        ],
	  },
	     // 默认用户信息
      userInfo: {
        jobId: "",
        name: "",
        sex: "",
        deptId: "",
        cardId: "",
        phone: "",
        education: "",
        email: "",
        tel: "",
        party: "",
        qqNum: "",
        address: "",
        postCode: "",
        birthday: "",
        race: "",
        speciality: "",
        hobby: "",
        remark: ""
      },
      // 获取需要更改的用户数据
      updateUser: []
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
          "name": val[0].name,
        }
      );
    },
    async getEmployee() {
      const { data: res } = await this.$http.post(
        "/api/employee/queryByCondition",
        {}
      );
      this.tableData = res.queryData.list;
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
    async  update(row) {
        this.empolyeeDialogVisible = !this.empolyeeDialogVisible;
        const { data: res } = await this.$http.post(
        "/api/employee/queryByCondition",
        {
          "name": row.name,
        }
      );
      this.updateUser = res.queryData.list;
      console.log(this.updateUser)
    },
    deleteEmployee(){
        this.getEmployee();
    },
    handleClose(done) {
        this.$confirm('确认关闭？')
          .then(_ => {
            done();
          })
          .catch(_ => {});
      },
      setRightDialogClosed(){
        // this.$refs.updateFormRef.resetFields();
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
.el-pagination {
  margin: 0 auto;
}
.options {
  display: inline;
}

.el-select{
	margin-bottom: 20px;
}

</style>
