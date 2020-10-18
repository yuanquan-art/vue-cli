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
               @click="updateNotice(scope.row)"
            />
        </el-table-column>
        <el-table-column prop="job" label="预览" width="120"> </el-table-column>
      </el-table>
    </el-card>

   <el-dialog
      title="更新员工"
      :visible.sync="empolyeeDialogVisible"
      width="70%"
      @close="setRightDialogClosed"
    >
      <el-form
        :model="addForm"
        :rules="addFormRules"
        ref="addFormRef"
        :inline="true"
      >
        <el-row>
          <el-col :span="8">
            <el-form-item label="姓名" prop="name">
              <el-input v-model="addForm.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="身份证号码" prop="cardId">
              <el-input v-model="addForm.cardId"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="8">
            性别：
            <div class="options">
              <el-select
                v-model="addForm.sex"
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
                v-model="addForm.jobId"
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
            <el-form-item label="学历">
              <el-input v-model="addForm.education"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="邮箱">
              <el-input v-model="addForm.email"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="8">
            <el-form-item label="手机">
              <el-input v-model="addForm.phone"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="电话">
              <el-input v-model="addForm.tel"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="8">
            <el-form-item label="政治面貌">
              <el-input v-model="addForm.party"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="QQ号码">
              <el-input v-model="addForm.qqNum"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="8">
            <el-form-item label="联系地址">
              <el-input v-model="addForm.address"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="邮政编码">
              <el-input v-model="addForm.postCode"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="8">
            <el-form-item label="出生日期">
              <el-input v-model="addForm.birthday"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="民族">
              <el-input v-model="addForm.race"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="8">
            <el-form-item label="所学专业">
              <el-input v-model="addForm.speciality"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="爱好">
              <el-input v-model="addForm.hobby"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

        <el-row>
          <el-col :span="8">
            <el-form-item label="备注">
              <el-input v-model="addForm.remark"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            所属部门：
            <div class="options">
              <el-select
                v-model="addForm.deptId"
                slot="prepend"
                placeholder="选择部门"
              >
                <el-option label="技术部" value="1"></el-option>
                <el-option label="管理部" value="2"></el-option>
              </el-select>
            </div>
          </el-col>
        </el-row>
        <el-row> </el-row>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="empolyeeDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="updateForm">更新</el-button>
      </span>
    </el-dialog>

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
      title: "",
       // 添加表单对象
      addForm: {
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
      //添加表单校验规则对象
     addFormRules: {
        name: [
          { required: true, message: "请输入活动名称", trigger: "blur" }
        ],
        cardId: [
          { required: true, message: "请输入活动名称", trigger: "blur" },
        ],
	  },
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
     const { data: res } = await this.$http.post(
        "/api/notice/deleteByCondition",
        {
          "title": this.title
        }
      );
      console.log(res);
      this.getNotice();
    },
    //更新公告
    updateNotice(){
       

      
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
