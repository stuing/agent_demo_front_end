<template>
  <div class="home">
    <h2>首页</h2>
    <p v-if="user">欢迎 {{ user.name }}</p>
    <p v-else>
      请 <router-link to="/login">登录</router-link>
      或 <router-link to="/register">注册</router-link>
    </p>
    <button v-if="user" @click="logout">退出登录</button>
  </div>
</template>

<script>
export default {
  data() {
    return { user: null };
  },
  created() {
    const saved = localStorage.getItem('currentUser');
    if (saved) {
      this.user = JSON.parse(saved);
    }
  },
  methods: {
    logout() {
      localStorage.removeItem('currentUser');
      this.user = null;
    }
  }
};
</script>

<style scoped>
.home {
  text-align: center;
}
</style>
