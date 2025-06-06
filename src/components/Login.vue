<template>
  <div class="login">
    <h2>登录</h2>
    <form @submit.prevent="handleLogin">
      <input v-model="form.username" type="text" placeholder="用户名" required />
      <input v-model="form.password" type="password" placeholder="密码" required />
      <button type="submit">登录</button>
    </form>
    <p>没有账号？<router-link to="/register">立即注册</router-link></p>
  </div>
</template>

<script>
import api from '../api.js'
export default {
  data() {
    return {
      form: {
        username: '',
        password: ''
      }
    };
  },
  methods: {
    async handleLogin() {
      try {
        const user = await api.post('/accounts/login', {
          username: this.form.username,
          password: this.form.password
        })
        localStorage.setItem('currentUser', JSON.stringify(user))
        alert('登录成功')
        this.$router.push('/home')
      } catch (err) {
        alert(err.message)
      }
    }
  }
};
</script>
