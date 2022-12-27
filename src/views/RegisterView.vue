<template>
  <div id="registerForm" style="width:500px;margin:auto">
    <h3>用户登录</h3>
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
        <el-form-item label="用户名" prop="name">
            <el-input  v-model="ruleForm.name"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="passWord">
            <el-input type="password" v-model="ruleForm.passWord"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
          <el-button @click="resetForm('ruleForm')">重置</el-button>
        </el-form-item>
        <el-form-item>
          没有账号请<router-link to="/login">注册</router-link>
        </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name:"LoginVue",
     data() {
      return {
        ruleForm: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: '',
          passWord:''
        },
        rules: {
          name: [
            { required: true, message: '请输入活动名称', trigger: 'blur' },
            { min: 3, max: 15, message: '长度在 3 到 5 个字符', trigger: 'blur' }
          ],
          passWord:[
            { required:true,message:'请输入密码',trigger:'blur' }
          ],
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            // get请求
            // this.axios.get('/',{
            //   // 数据会在url后附带
            //   params:{
                
            //   }
            // }).then(res=>console.log(res))
            // .catch(res=>console.log(res))
            // post请求
            this.axios({
              method:"post",
              url:"/api/register",
              data:{
                userName: this.ruleForm.name,
                passWord: this.ruleForm.passWord
              },
            }).then(res=>{
              console.log("then...");
              console.log(res)
              this.$message({
                message:"登录成功",
                type:"success"
              });
              localStorage.setItem("userName",res.data.userName)
              localStorage.setItem("token",res.data.password)
              this.$router.push('/home')
            }).catch(res=>{
              console.log("catch...")
              console.log(res)
              if(res.response.status == 400)
              this.$message.error('登录失败,用户名或密码错误');
              if(res.response.status == 500)
              this.$message.error('登录失败，服务器异常')
            })
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
}
</script>

<style>
#registerForm{
  position: absolute;
  top: 30%;
  left: 43%;
  padding: 30px;
  padding-right: 40px;
  border: 3px slategray solid;
  border-radius: 30px;
}
</style>