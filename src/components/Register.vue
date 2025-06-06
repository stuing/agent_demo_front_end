<template>
  <div class="register">
    <h2>注册</h2>
    <form @submit.prevent="handleRegister">
      <input v-model="form.name" type="text" placeholder="姓名" required />
      <input v-model="form.email" type="email" placeholder="邮箱" required />
      <input v-model="form.password" type="password" placeholder="密码" required />
      <button type="submit">注册</button>
    </form>
    <p>已有账号？<router-link to="/login">立即登录</router-link></p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        email: '',
        password: ''
      }
    };
  },
  methods: {
    handleRegister() {
      const users = JSON.parse(localStorage.getItem('users') || '[]')
      if (users.some((u) => u.email === this.form.email)) {
        alert('邮箱已存在')
        return
      }
      users.push({ ...this.form })
      localStorage.setItem('users', JSON.stringify(users))
      alert('注册成功，请登录')
      this.$router.push('/login')
    }
  }
};
</script>
