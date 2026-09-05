<template>
    <div style="padding: 20px;">
        <h2>Daftar Akun Baru</h2>
        <form @submit.prevent="handleRegister">
            <div style="margin-bottom: 10px;">
                <label>Username (Min. 3 karakter):</label><br>
                <input v-model="username" type="text" required style="padding: 5px;" />
            </div>

            <div style="margin-bottom: 15px;">
                <label>Password (Min. 8 karakter):</label><br>
                <input v-model="password" type="password" required style="padding: 5px;" />
            </div>

            <button type="submit" style="padding: 5px 15px; cursor: pointer;">Daftar</button>
        </form>
        <p style="margin-top: 15px;">Sudah punya akun? <router-link to="/login">Login di sini</router-link></p>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import api from '../axios';

const username = ref('');
const password = ref('');
const router = useRouter();

const handleRegister = async () => {
    try {
        await api.post('/user/register', {
            username: username.value,
            password: password.value
        });
        alert('Registrasi berhasil! Silakan login.');
        router.push('/login');
    } catch (error) {
        alert(error.response?.data?.error || 'Registrasi gagal!');
    }
};
</script>