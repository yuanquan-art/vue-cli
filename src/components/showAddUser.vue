<template>
    <div>
		<!-- 面包屑导航区域 -->
		<el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>用户管理</el-breadcrumb-item>
      <el-breadcrumb-item>用户添加</el-breadcrumb-item>
    </el-breadcrumb>
		<!-- 卡片视图区域 -->
    <el-card class="box-card">
		
      <!-- 添加和搜索 -->
      <el-row :gutter="10">
        <el-col :span="12"
          ><div>
            姓名：<el-input
              label="姓名"
              placeholder="请输入内容"
            ></el-input></div
        ></el-col>
        <el-col :span="12"
          ><div>
            状态：<el-select
              v-model="select"
              slot="prepend"
              placeholder="全部"
            >
              <el-option label="管理员" value="1"></el-option>
              <el-option label="普通用户" value="2"></el-option>
            </el-select></div>
        </el-col>
      </el-row>
	  <el-row :gutter="10">
        <el-col :span="12"
          ><div>
            登录名：<el-input
              placeholder="请输入内容"
            ></el-input></div
        ></el-col>
        <el-col :span="12">
			<div>
            密码: <el-input
              placeholder="请输入内容"
            ></el-input>
			</div>
        </el-col>
      </el-row>
	  <el-row :gutter="10"> 
		  <el-col :span="2">
			  <el-button round type="primary">添加</el-button>
		  </el-col>
		  <el-col :span="2">
			  <el-button type="danger" icon="el-icon-delete" circle></el-button>
		  </el-col>
	  </el-row>
    </el-card>
	</div>
</template>

<script>
export default {};
</script>

<style lang ='less'scoped>
.el-input{
  width: 300px;
}
.el-row{
  margin-bottom: 15px;
}
</style>