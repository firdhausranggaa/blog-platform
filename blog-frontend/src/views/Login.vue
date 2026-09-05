<template>
    <div style="padding: 20px;">
        <h2>Login Pengguna</h2>
        <input v-model="username" placeholder="Username" style="display:block; margin-bottom:10px;" />
        <input type="password" v-model="password" placeholder="Password" style="display:block; margin-bottom:10px;" />
        <button @click="handleLogin">Masuk</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import api from '../axios';
import { authState } from '../store';

const username = ref('');
const password = ref('');
const router = useRouter();

const handleLogin = async () => {
    try {
        const response = await api.post('/user/login', {
            username: username.value,
            password: password.value
        });

        authState.isLoggedIn = true;
        authState.username = response.data.username;

        alert('Login berhasil!');
        router.push('/');
    } catch (error) {
        alert(error.response?.data?.error || 'Login gagal!');
    }
};
</script>