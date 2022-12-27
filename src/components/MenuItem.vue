<template>
  <div>
    <el-menu :default-openeds="['1', '3']">
      <el-submenu index="1">
        <template slot="title"
          ><i class="el-icon-message"></i>用户管理</template
        >
        <el-menu-item-group>
          <el-menu-item index="1-1">用户列表</el-menu-item>
        </el-menu-item-group>
      </el-submenu>
      <el-submenu index="2">
        <template slot="title"><i class="el-icon-menu"></i>房间管理</template>
        <el-menu-item-group>
          <el-menu-item index="2-1">房间状态</el-menu-item>
        </el-menu-item-group>
      </el-submenu>
      <el-submenu index="3">
        <template slot="title"
          ><i class="el-icon-setting"></i>收银管理</template
        >
        <el-menu-item-group>
          <el-menu-item index="3-1">收入统计</el-menu-item>
          <el-menu-item index="3-2">支出统计</el-menu-item>
        </el-menu-item-group>
        <el-menu-item-group>
          <el-menu-item index="3-3">利润统计</el-menu-item>
        </el-menu-item-group>
      </el-submenu>
    </el-menu>
  </div>
</template>

<script>
export default {
  name: "MenuItem",
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
  },
};
</script>

<style>
</style>