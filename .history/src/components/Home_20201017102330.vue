<template> 
 <!-- 整个页面区域 -->
  <el-container>
      <!-- 页面标题 -->
  <el-header>
      <div>
          <img src="../assets/images/icon.png" alt="">
          <span>CSI员工之家系统</span>
          <span class="user">张三</span>
      </div>
      <el-button type="info" @click="logout">退出</el-button>
  </el-header>
  <!-- 页面主体部分 -->
  <el-container>
    <el-aside :width="isCollapse? '64px' : '200px'">
        <div class="collapse" @click="toggleCollapse">|||</div>
        <!-- 侧边栏菜单区域 -->
       <el-menu
      background-color="rgb(91, 188, 233)"
      text-color="#000"
      active-text-color="#409bff"
      :unique-opened="true"
      :collapse="isCollapse"
      :collapse-transition="false"
      router
      :default-active="activePath">
      <!-- 一级菜单 -->
      <el-submenu :index="item.id+''" v-for="item in menulist" :key="item.id">
          <!-- 一级菜单模板区域 -->
        <template slot="title">
            <!-- 图标 -->
          <i :class="iconsObj[item.id]"></i>
             <!-- 文本 -->
          <span>{{ item.authName }}</span>
        </template>
        <!-- 二级菜单 -->
        <el-menu-item 
        :index="'/'+subItem.path" 
        v-for="subItem in item.children"
        :key='subItem.id'
        @click="savNavState('/'+subItem.path)">
            <template slot="title">
            <!-- 图标 -->
          <i class="el-icon-menu"></i>
             <!-- 文本 -->
          <span>{{ subItem.authName }}</span>
        </template>
        </el-menu-item>
      </el-submenu>
    </el-menu>
    </el-aside>
    <el-main>
        <router-view></router-view>
    </el-main>
  </el-container>
</el-container>

</template>

<script>
export default {
    data () {
        return {
            // 左侧菜单数据
            menulist: [
                {
            "id": 101,
            "authName": "用户管理",
            "path": '/home',
            "children": [
                {
                    "id": 104,
                    "authName": "用户查询",
                    "path": 'users',
                    "children": []
                },
                {
                    "id": 104,
                    "authName": "添加用户",
                    "path": 'adduser',
                    "children": []
                }
            ]
        },
         {
            "id": 102,
            "authName": "部门管理",
            "path": '/home',
            "children": [
                {
                    "id": 104,
                    "authName": "部门查询",
                    "path": 'updatedept',
                    "children": []
                },
                {
                    "id": 104,
                    "authName": "添加部门",
                    "path": 'adddept',
                    "children": []
                }
            ]
        },
         {
            "id": 103,
            "authName": "职位管理",
            "path": '/home',
            "children": [
                {
                    "id": 104,
                    "authName": "职位查询",
                    "path": 'updatejob',
                    "children": []
                },
                {
                    "id": 104,
                    "authName": "添加职位",
                    "path": 'addjob',
                    "children": []
                }
            ]
         },
          {
            "id": 104,
            "authName": "员工管理",
            "path": '/home',
            "children": [
                {
                    "id": 104,
                    "authName": "员工查询",
                    "path": 'employee',
                    "children": []
                },
                {
                    "id": 104,
                    "authName": "添加员工",
                    "path": 'addEmployee',
                    "children": []
                }
            ]
        },
         {
            "id": 105,
            "authName": "公告管理",
            "path": '/home',
            "children": [
                {
                    "id": 104,
                    "authName": "公告查询",
                    "path": 'notice',
                    "children": []
                },
                {
                    "id": 104,
                    "authName": "添加公告",
                    "path": 'addNotice',
                    "children": []
                }
            ]
        },
         {
            "id": 106,
            "authName": "下载中心",
            "path": '/home',
            "children": [
                {
                    "id": 104,
                    "authName": "文档查询",
                    "path": 'document',
                    "children": []
                },
                {
                    "id": 104,
                    "authName": "上传文档",
                    "path": 'addDocument',
                    "children": []
                }
            ]
        }
            ],
            // 自定义字体图标
            iconsObj: {
                '101': 'iconfont icon-shangpin',
                '102': 'iconfont icon-danju',
                 '103': 'iconfont icon-tijikongjian',
                '104': 'iconfont icon-user',
                '105': 'iconfont baobiao',
                '106': 'iconfont baobiao'
            },
            // 是否折叠
            isCollapse: false,
            // 被激活的链接
            activePath: ''
        }
    },
    created () {
       this.getMenuList();
       this.activePath = window.sessionStorage.getItem('activePath');
    },
    methods: {
        // 自定义方法
        logout () {
            // 清空token
            window.sessionStorage.clear();
            // 编程式导航重定向
            this.$router.push('/login');
        },
       // 点击按钮折叠菜单栏
       toggleCollapse () {
         this.isCollapse = ! this.isCollapse;
       },
       //保存导航链接的激活状态
       savNavState (activePath) {
          window.sessionStorage.setItem('activePath',activePath);
          this.activePath = activePath;
       }
    }
}
</script>

<style lang="less" scoped>
.el-container {
    height: 100%;
}
.el-header {
    background-color: rgb(82, 11, 141);
    display: flex;
    justify-content: space-between;
    align-items: center;
    > div {
        display: flex;
        align-items: center;
        color: #fff;
        font-size: 30px;
        span {
            padding-left: 10px;
        }
    }
}
.el-aside {
    background-color: rgb(91, 188, 233);
    .el-menu {
        border-right: 0;
    }
}
.el-main {
    background-color: rgb(22, 226, 114);
}
.iconfont {
    margin-right: 10px;
}
.collapse {
    height: 20px;
    background-color: rgb(255, 0, 221);
    text-align: center;
    line-height: 20px;
    font-size: 10px;
}
.user{
    margin: 0 auto;
}
</style>