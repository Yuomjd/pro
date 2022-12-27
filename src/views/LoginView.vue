<template>
  <div id="loginForm">
    <h3>用户注册</h3>
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
        <el-form-item label="用户名" prop="name">
            <el-input  v-model="ruleForm.name"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="passWord">
            <el-input type="password" v-model="ruleForm.passWord"></el-input>
        </el-form-item>
        <el-form-item label="确认密码" prop="checkPass">
          <el-input type="password" v-model="ruleForm.checkPass" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item prop="trueName" label="真实姓名">
          <el-input v-model="ruleForm.trueName"></el-input>
        </el-form-item>
        <el-form-item prop="email" label="邮箱">
          <el-input v-model="ruleForm.email"></el-input>
        </el-form-item>
        <el-form-item prop="idCard" label="身份证号">
          <el-input v-model="ruleForm.idCard"></el-input>
        </el-form-item>
        <el-form-item label="性别" prop="gender">
          <el-radio-group v-model="ruleForm.gender">
            <el-radio label="男"></el-radio>
            <el-radio label="女"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')">注册</el-button>
          <el-button @click="resetForm('ruleForm')">重置</el-button>
           <el-button @click="goRegister()">去登录</el-button>
        </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name:"LoginVue",
     data() {
      var validatePass2 = (rule, value, callback) => {
      if (value === '') {
          callback(new Error('请再次输入密码'));
        } else if (value !== this.ruleForm.passWord) {
          callback(new Error('两次输入密码不一致!'));
        } else {
          callback();
        }
      };
      return {
        ruleForm: {
          name: '',
          passWord:'',
          email:'',
          trueName:'',
          idCard:'',
          gender:'',
        },
        rules: {
          name: [
            { required: true, message: '请输入活动名称', trigger: 'blur' },
            { min: 3, max: 15, message: '长度在 3 到 5 个字符', trigger: 'blur' }
          ],
          passWord:[
            { required:true,message:'请输入密码',trigger:'blur' }
          ],
          checkPass:[
            {validator:validatePass2,trigger:'blur'}
          ],
          email:[
            { required: true, message: '请输入邮箱地址', trigger: 'blur' },
            { type: 'email', message: '请输入正确的邮箱地址', trigger: ['blur', 'change'] }
          ],
          idCard:[
            { required:true,message:'请输入身份证号',trigger:'blur' },
            { min:18, max:18, message:'请输入正确的身份证号', trigger:'blur' }
          ],
          gender:[
             { required: true, message: '请选择性别', trigger: 'blur' },
          ],
          trueName:[
            { required: true,message: '请输入真实姓名', trigger: 'blur' },
            {min:2,max:15,message:'请输入真实的姓名',trigger:'blur'}
          ]
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
              url:"/api/login",
              data:{
                userName: this.ruleForm.name,
                passWord: this.ruleForm.passWord,
                email: this.ruleForm.email,
                gender: this.ruleForm.gender,
                idCard: this.ruleForm.idCard,
                trueName: this.ruleForm.trueName
              },
            }).then(res=>{
              console.log("then...");
              console.log(res)
              this.$message({
                message:"注册成功",
                type:"success"
              });
              console.log(res.data);
              localStorage.setItem("userName",res.data.userName)
              localStorage.setItem("token",res.data.password)
              this.$router.push('/home')
            }).catch(res=>{
              console.log("catch...")
              console.log(res)
              if(res.response.status == 400)
              this.$message.error('注册失败,用户名重复');
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
      },
      goRegister(){
        this.$router.push('/register');
      }
    }
}
</script>

<style>
#loginForm{
  position: absolute;
  top: 30%;
  left: 43%;
  padding: 30px;
  padding-right: 40px;
  border: 3px slategray solid;
  border-radius: 30px;
}

</style>