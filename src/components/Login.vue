<template>
  <div class="mui-content">
    <el-card class="box-card">
      <div slot="header">
        <span>用户登录</span>
      </div>
      <div>
        <el-form :model="user" :rules="rules" ref="user" label-width="100px" class="demo-ruleForm">
          <el-form-item label="用户名" prop="username">
            <el-input v-model="user.username"></el-input>
          </el-form-item>
          <el-form-item label="密码" prop="password">
            <el-input type="password" v-model="user.password"></el-input>
          </el-form-item>
          <el-form-item style="display: flex;align-content: center;margin-left: 50px">
            <el-button type="primary" @click="login('user')">登录</el-button>
            <el-button @click="resetForm('user')">重置</el-button>
          </el-form-item>
        </el-form>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      user: {
        username: '',
        password: ''
      },
      rules: {
        username: [
          {required: true, message: '请输入用户名', trigger: 'blur'},
          {min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur'}
        ],
        password: [
          {required: true, message: '请输入密码', trigger: 'blur'},
          {min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur'}
        ]
      }
    };
  },
  methods: {
    login(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.postRequest("/login", this.user).then(resp => {
            console.log(resp);
            if (resp) {
              this.$router.push("/home");
            }
          });
          /*alert('登陆成功!');
          this.$router.push("/home");*/
        } else {
          console.log('登陆失败');
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  html,body{
    width: 100%;
    height: 100%;
    padding: 0px;
  }

  .mui-content{
    background: url(../assets/bg111.png) bottom center no-repeat #efeff4 ;
    background-size: 100% 100%;
    width: 100%;
    position: fixed;
    height: 100%;
    display: flex;
    justify-content: center;
  }
  .box-card {
    background: aliceblue;
    color: #2c3e50;
    width: 480px;
    height: 280px;
    margin-top: 600px;
  }

</style>
