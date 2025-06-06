<template>
  <div class="register">
    <h2>注册</h2>
    <form @submit.prevent="handleRegister">
      <input v-model="form.username" type="text" placeholder="用户名" required />
      <input v-model="form.email" type="email" placeholder="邮箱" required />
      <input v-model="form.phone" type="tel" placeholder="手机号" required />
      <input v-model="form.password" type="password" placeholder="密码" required />
      <button type="submit">注册</button>
    </form>
    <p>已有账号？<router-link to="/login">立即登录</router-link></p>
  </div>
</template>

<script>
import api from '../api.js'
export default {
  data() {
    return {
      form: {
        username: '',
        email: '',
        phone: '',
        password: ''
      }
    };
  },
  methods: {
    async handleRegister() {
      try {
        await api.post('/accounts', {
          username: this.form.username,
          password: this.form.password,
          email: this.form.email,
          phone: this.form.phone
        })
        alert('注册成功，请登录')
        this.$router.push('/login')
      } catch (err) {
        alert(err.message)
      }
    }
  }
};
</script>
