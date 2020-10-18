<template>
  <div>
    <!-- 面包屑导航 -->
    <el-breadcrumb separator="/">
      <el-breadcrumb-item>当前位置：公告管理</el-breadcrumb-item>
      <el-breadcrumb-item><a href="/">添加公告</a></el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 卡片区域 -->
    <el-card>
      <el-row>
        <el-col :span="8">
          公告标题：
          <el-input v-model="addForm.title"></el-input>
        </el-col>
      </el-row>
      公告内容：
      <el-row>
        <el-col :span="16">
          <el-input type="textarea" rows="10" v-model="addForm.title"></el-input>
        </el-col>
      </el-row>

      <el-button @click="addNotice">添加</el-button>
      <el-button>重置</el-button>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 添加表单对象
      addForm: {
        title: "",
        content: "",
      },
    };
  },
  methods: {
	 async addNotice(){
		  const { data: res } = await this.$http.post(
        "/api/notice/queryByCondition",
        this.notice
      );
	 }
  }
};
</script>

<style lang="less" scoped>
.el-input {
  width: 250px;
}
</style>
