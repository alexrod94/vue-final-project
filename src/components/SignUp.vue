<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import { useUserStore } from '../store/user.js'

const router = useRouter()
const email = ref('')
const password = ref('')
const confirmPassword = ref('')
const errorMsg = ref(null)

const userStore = useUserStore()

async function signUp() {
  if (password.value && email.value && confirmPassword.value) {
    try {
      await userStore.signUp(email.value, password.value, confirmPassword.value)
      router.push({ path: '/' })
    } catch (e) {
      console.log('error')
      errorMsg.value = 'Could not sign you up please contact support'
    }
  } else {
    errorMsg.value = 'Please enter valid login details';
  }
}
</script>

<template>
  <article class="auth-article">
    <div
      v-if="errorMsg"
      class="error"
    >
      {{ errorMsg }}
    </div>
    <form
      class="register"
      @submit.prevent="signUp"
    >
      <h3>Sign Up</h3>
      <div>
        <label for="email">Email</label><br>
        <input 
          v-model="email"
          type="email" 
          name="email"
          required
          placeholder="Email"
        ><br>
        <label for="password">Password</label><br>
        <input 
          v-model="password" 
          type="password"
          name="password" 
          required
          placeholder="Password"
        ><br>
        <label for="confirmPassword">Repeat Password</label><br>
        <input 
          v-model="confirmPassword" 
          type="password"
          name="confirmPassword" 
          required
          placeholder="Repeat Password"
        ><br>
        <button type="submit">
          Register
        </button>
      </div>
    </form>
  </article>
</template>

<style scoped>
.register {
    display: grid;
}
</style>
