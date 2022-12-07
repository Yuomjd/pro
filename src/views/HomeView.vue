<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <el-table
      :data="userList"
      style="width: 100%">
      <el-table-column
        prop="userId"
        label="日期"
        width="180">
      </el-table-column>
      <el-table-column
        prop="title"
        label="姓名"
        width="180">
      </el-table-column>
      <el-table-column
        prop="id"
        label="地址">
      </el-table-column>
    </el-table>
  </div>
  
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  data:function(){
    return{
      userList:{
        userId:Number,
        id:Number,
        title:String,
        completed:Boolean
      }
    }
  },
  components: {
    HelloWorld
  },
  created(){
    this.load()
  },
  methods:{
    load(){
      this.axios({
        method:"get",
        url:"http://jsonplaceholder.typicode.com/todos",
      }).then(res=>{
        console.log(res);
        this.userList = res.data
      })
    }
  }
}
</script>
