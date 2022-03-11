<script setup>
import { ref } from 'vue'

import SignIn from "../components/SignIn.vue";
import SignUp from "../components/SignUp.vue";

const signup = ref(false)
</script>

<template>
  <article class="auth">
    <nav class="buttons">
      <button
        v-if="!signup"
        id="signup"
        @click="signup=true"
      >
        Click to Sign Up
      </button>
      <button
        v-if="signup"
        id="signin"
        @click="signup=false"
      >
        Click to Sign In
      </button>
    </nav>
    <SignIn v-if="!signup" />
    <SignUp v-if="signup" />
  </article>
</template>


<style scoped>
.auth {
    display: grid;
    padding: 2rem;
    justify-content: center;
}
.buttons {
    display: grid;
    margin-bottom: 2rem;
}
button {
    background: none;
    border: none;
    border-bottom: solid 2px;
}
button:hover {
    border-bottom: solid 2px lightgray
}
</style>
