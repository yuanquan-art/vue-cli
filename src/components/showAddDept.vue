<template>
    <div>
		<!-- 面包屑导航区域 -->
		<el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>部门管理</el-breadcrumb-item>
      <el-breadcrumb-item>部门添加</el-breadcrumb-item>
    </el-breadcrumb>
		<!-- 卡片视图区域 -->
    <el-card class="box-card">
		
      <!-- 添加和搜索 -->
      <el-row :gutter="10">
        <el-col :span="12"
          ><div>
            部门名称：<el-input
              placeholder="请输入内容"
            ></el-input></div
        ></el-col>
        <el-col :span="12"
          ><div>
            详细描述：<el-input placeholder="请输入内容"></el-input>
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

<style lang="less" scoped>
.el-input{
  width: 400px;
}
.el-row{
  margin-bottom: 15px;
}
</style>