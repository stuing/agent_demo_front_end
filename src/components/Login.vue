<template>
  <div class="login">
    <h2>登录</h2>
    <form @submit.prevent="handleLogin">
      <input v-model="form.email" type="email" placeholder="邮箱" required />
      <input v-model="form.password" type="password" placeholder="密码" required />
      <button type="submit">登录</button>
    </form>
    <p>没有账号？<router-link to="/register">立即注册</router-link></p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        email: '',
        password: ''
      }
    };
  },
  methods: {
    handleLogin() {
      const users = JSON.parse(localStorage.getItem('users') || '[]')
      const user = users.find(
        (u) => u.email === this.form.email && u.password === this.form.password
      )
      if (user) {
        localStorage.setItem('currentUser', JSON.stringify(user))
        alert('登录成功')
        this.$router.push('/home')
      } else {
        alert('邮箱或密码错误')
      }
    }
  }
};
</script>
