<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <el-container>
      <el-header>Header</el-header>
      <el-container>
        <el-aside width="200px"><menu-item></menu-item></el-aside>
        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import MenuItem from '@/components/MenuItem.vue';
// @ is an alias to /src


export default {
  name: "HomeView",
  data: function () {
    return {
      userList: {
        userId: Number,
        id: Number,
        title: String,
        completed: Boolean,
      },
    };
  },
  components: {
    MenuItem,
  },
};
</script>

<style>
 .el-header, .el-footer {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
  }
  
  .el-aside {

    color: #333;
    text-align: center;
    line-height: 200px;
  }
  
  .el-main {

    color: #333;
    text-align: center;
    line-height: 160px;
  }
  
  body > .el-container {
    margin-bottom: 40px;
  }
  
  .el-container:nth-child(5) .el-aside,
  .el-container:nth-child(6) .el-aside {
    line-height: 260px;
  }
  
  .el-container:nth-child(7) .el-aside {
    line-height: 320px;
  }
</style>
