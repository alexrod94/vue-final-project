<template>
  <section class="app-container">
    <AppHeader class="app-header" />
    <Nav class="main-nav" />
    <router-view class="app-main" />    
  </section>
</template>

<script setup>
import { onMounted } from 'vue'
import { storeToRefs } from 'pinia'
import { useRouter } from 'vue-router'
import { useUserStore } from './store/user.js'

import AppHeader from "./components/AppHeader.vue"
import Nav from "./components/Nav.vue"

const router = useRouter()

const userStore = useUserStore()
const { user } = storeToRefs(userStore)

onMounted(async () => {
  try {
    await userStore.fetchUser()
    if (!user.value) {
      router.push({ path: '/auth' });
    } else {
      router.push({ path: '/' });
    }
  } catch (e) {
    console.log(e)
  }
})
</script>

<style>
.app-container {
  display: grid;
  grid-template-columns: 1fr 2fr 2fr 1fr;
  grid-template-areas: 
  "hd hd hd hd"
  ". nav nav ."
  ". main main .";
}

.app-header {
  grid-area: hd;
}

.app-main {
  grid-area: main;
  background: white;
  margin-top: 2rem;
}

.main-nav {
  grid-area: nav;
}
</style>
