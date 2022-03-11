<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import { useUserStore } from '../store/user.js'

const router = useRouter()
const email = ref('')
const password = ref('')
const errorMsg = ref(null)
const userStore = useUserStore()

async function signIn() {
  if (password.value && email.value) {
    try {
      await userStore.signIn(email.value, password.value)
      router.push({ path: '/' })
    } catch (e) {
      errorMsg.value = e.message
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
      @submit.prevent="signIn"
    >
      <h3>Sign In</h3>
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
        <button type="submit">
          Log In
        </button>
      </div>
    </form>
  </article>
</template>
