<template>
  <el-row type="flex">
    <el-col :xs="0" :sm="6" :md="6" :lg="9" :xl="10"></el-col>
    <el-col :xs="24" :sm="12" :md="12" :lg="6" :xl="4">
      <el-card shadow="always" class="box-card">
        <el-form :model="form" :rules="rules" label-position="top" ref="form" label-width="120px">
          <el-form-item label="Username" prop="username">
            <el-input type="text" v-model="form.username" />
          </el-form-item>
          <el-form-item label="Password" prop="password">
            <el-input type="password" v-model="form.password" />
          </el-form-item>
          <!-- Optional "Remember me" checkbox if necessary -->
          <!-- <el-form-item prop="type">
            <el-checkbox label="Remember me" name="type"></el-checkbox>
          </el-form-item>-->
        </el-form>
        <div class="bottom clearfix">
          <el-button
            style="float:right"
            type="primary"
            icon="el-icon-unlock"
            :disabled="loggingIn"
            @click="handleLogin"
          >Login</el-button>
        </div>
      </el-card>
    </el-col>
    <el-col :xs="0" :sm="6" :md="6" :lg="9" :xl="10"></el-col>
  </el-row>
</template>

<script>
export default {
  data() {
    return {
      form: { username: "", password: "" },
      submitted: false,
      rules: {
        username: [
          {
            required: true,
            message: "Please input your user name",
            trigger: "blur"
          }
        ],
        password: [
          {
            required: true,
            message: "Please input your password",
            trigger: "blur"
          }
        ]
      }
    };
  },
  computed: {
    loggingIn() {
      return this.$store.state.authentication.status.loggingIn; //hook up to store
    }
  },
  created() {
    // reset login status
    this.$store.dispatch("authentication/logout"); //hook up to action
  },
  methods: {
    handleLogin(e) {
      this.submitted = true;
      var username = this.form.username;
      var password = this.form.password;
      const { dispatch } = this.$store;
      if (this.form.username && this.form.password) {
        dispatch("authentication/login", { username, password }); //hook up to action
      }
    }
  }
};
</script>
