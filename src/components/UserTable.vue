<template>
  <div>
    <el-table :data="userList">
      <el-table-column prop="userId" label="用户id" width="140">
      </el-table-column>
      <el-table-column prop="userName" label="用户名" width="120">
      </el-table-column>
      <el-table-column prop="trueName" label="真实姓名"> </el-table-column>
      <el-table-column prop="gender" label="性别"> </el-table-column>
      <el-table-column prop="contact" label="联系方式"> </el-table-column>
      <el-table-column prop="idCard" label="身份证号"> </el-table-column>
      <el-table-column label="操作">
        <el-button type="primary" icon="el-icon-edit" circle></el-button>
        <el-button type="danger" icon="el-icon-delete" circle></el-button>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: "UserTable",
  data: function () {
    return {
      userList: [
        {
          userId: "",
          userName: "",
          trueName: "",
          gender: "",
          contact: "",
          userTyp: "",
          idCard: "",
        },
      ],
    };
  },
  methods: {
    getUserList() {
      this.axios
        .get("/api/user", {
          // 数据会在url后附带
          params: {},
        })
        .then((res) => {
          this.userList = res.data;
        })
        .catch((res) => console.log(res));
    },
  },
  created() {
    this.getUserList();
  },
};
</script>

<style>
</style>