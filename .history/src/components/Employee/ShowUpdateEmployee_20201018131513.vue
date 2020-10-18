<template>
  <div>
    <!-- 面包屑导航 -->
    <el-breadcrumb separator="/">
      <el-breadcrumb-item>当前位置：员工管理</el-breadcrumb-item>
      <el-breadcrumb-item><a href="/">添加员工</a></el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 表单 -->
    <el-card>
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
            <el-form-item label="身份证号码" prop="IdNumber">
              <el-input v-model="addForm.IdNumber"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
    <!-- 选择框 -->
	<el-row>
		<el-col :span="8">
           性别：
	  <el-select v-model="value" placeholder="男">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
          </el-option>
        </el-select>
		</el-col>
		<el-col :span="8">
              职位：
	  <el-select v-model="value" placeholder="职员">
          <el-option
            v-for="item in optionsJob"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
          </el-option>
        </el-select>
		</el-col>
	</el-row>
	

        <el-row>
          <el-col :span="8">
            <el-form-item label="学历" prop="name">
              <el-input v-model="addForm.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="邮箱" prop="IdNumber">
              <el-input v-model="addForm.IdNumber"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

		<el-row>
          <el-col :span="8">
            <el-form-item label="手机" prop="name">
              <el-input v-model="addForm.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="电话" prop="IdNumber">
              <el-input v-model="addForm.IdNumber"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

   <el-row>
          <el-col :span="8">
            <el-form-item label="政治面貌" prop="name">
              <el-input v-model="addForm.name"></el-input>
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
            <el-select v-model="value" placeholder="技术部">
          <el-option
            v-for="item in optionsDoor"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
          </el-option>
        </el-select>
          </el-col>
        </el-row>
        <el-row>
			<el-button>添加</el-button>
			<el-button>取消</el-button>
		</el-row>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
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
	    
    };
  },
};
</script>

<style lang="less" scoped>
.el-card{
	margin-top: 20px;
}
.el-input {
  width: 250px;
}
.el-select{
	margin-bottom: 20px;
}
.el-button{
	margin-left: 20px;
}
</style>
