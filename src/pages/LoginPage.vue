<template>
  <form @submit.prevent="onFormSubmit" class="auth-form login-form">
    <div class="form-field">
      <label for="login">Login</label>
      <input v-model="login" id="login" type="text" required/>
    </div>
    <div class="form-field">
      <label for="password">Password</label>
      <input v-model="password" id="password" type="text" required/>
    </div>
    <button class="submit-btn" type="submit">Войти</button>
    <div class="action-link">
      <span>Нет аккаунта?</span>
      <a @click="redirect" class="link-btn">Зарегистрируйтесь</a>
    </div>
  </form>
</template>

<script>
//import {doLogin} from "@/netClient/todoService";
import {doLogin} from "@/netClient/authService";

export default {
  name: 'LoginPage',
  data: () => ({
    login: '',
    password: '',
  }),
  async mounted() {
  },
  methods: {
    async onFormSubmit() {
      try {
        const accessToken = await doLogin(
            this.login.trim(),
            this.password.trim());
        console.warn({accessToken});
        if (accessToken) {
          this.$router.push("/");
        }
      } catch (error) {
        console.error({error});
      }
    },
    redirect() {
      this.$router.push("/registration");
    },
  },
};
</script>

<style scoped>
</style>
