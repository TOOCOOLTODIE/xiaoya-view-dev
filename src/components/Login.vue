<template>
  <div>
    <el-form
      :rules="rules"
      class="login-container"
      label-position="left"
      :model="loginForm"
      label-width="0px"
      v-loading="loading"
    >
      <h3 class="login_title">小雅</h3>
      <el-form-item prop="username">
        <el-input
          type="text"
          v-model="loginForm.username"
          auto-complete="off"
          placeholder="账号"
        ></el-input>
      </el-form-item>
      <el-form-item prop="password">
        <el-input
          type="password"
          v-model="loginForm.password"
          auto-complete="off"
          placeholder="密码"
        ></el-input>
      </el-form-item>
      <el-form-item style="width: 100%">
        <el-button type="primary" style="width: 100%" @click="submitClick"
          >登录</el-button
        >
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      rules: {
        username: [
          { required: true, message: "请输入用户名", trigger: "blur" }
        ],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }]
      },
      checked: true,
      loginForm: {
        username: "admin",
        password: "123"
      },
      loading: false
    };
  },
  methods: {
    submitClick() {
      var _this = this;
      this.loading = true;
      this.postRequest("login", {
        name: "admin",
        password: "123"
      }).then(resp => {
        var data = resp.data;
        _this.loading = false;
        if (resp && data.status == 200) {
          _this.$store.commit("login", data.obj);
          console.log("_this.$store", _this.$store);
          var path = _this.$route.query.redirect;
          _this.$router.replace({
            path: path == "/" || path == undefined ? "/blogmng/home" : path
          });
        } else {
          alert(data.msg);
          _this.$router.replace("/");
        }
      });
    }
  }
};
</script>
<style>
.login-container {
  border-radius: 15px;
  background-clip: padding-box;
  margin: 180px auto;
  width: 350px;
  padding: 35px 35px 15px 35px;
  background: #fff;
  border: 1px solid #eaeaea;
  box-shadow: 0 0 25px #cac6c6;
}
.login_title {
  margin: 0px auto 40px auto;
  text-align: center;
  color: #505458;
}
.login_remember {
  margin: 0px 0px 35px 0px;
  text-align: left;
}
</style>
