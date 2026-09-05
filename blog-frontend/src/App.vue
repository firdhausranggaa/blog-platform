<template>
  <nav style="padding: 20px; background: #f4f4f4; display: flex; gap: 15px; align-items: center;">
    <router-link to="/">Home</router-link>

    <template v-if="authState.isLoggedIn">
      <span>| Halo, <b>{{ authState.username }}</b>!</span>
      <router-link to="/create">Buat Artikel</router-link>
      <button @click="handleLogout"
        style="background: red; color: white; border: none; padding: 5px 10px; cursor: pointer;">
        Logout
      </button>
    </template>

    <template v-else>
      <span>|</span>
      <router-link to="/login">Login</router-link> |
      <router-link to="/register">Register</router-link>
    </template>
  </nav>

  <router-view></router-view>
</template>

<script setup>
import { onMounted } from 'vue';
import { useRouter } from 'vue-router';
import api from './axios';
import { authState } from './store';

const router = useRouter();

onMounted(async () => {
  try {
    const response = await api.get('/user/me');
    authState.isLoggedIn = true;
    authState.username = response.data.username;
  } catch (error) {
    authState.isLoggedIn = false;
  }
});

const handleLogout = async () => {
  try {
    await api.post('/user/logout');
    authState.isLoggedIn = false;
    authState.username = '';
    alert('Berhasil Logout');
    router.push('/login');
  } catch (error) {
    console.error("Gagal logout:", error);
  }
};
</script>