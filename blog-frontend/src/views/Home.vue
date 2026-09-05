<template>
    <div style="padding: 20px;">
        <h1>Daftar Artikel Blog</h1>
        <div v-if="posts.length === 0">Belum ada artikel.</div>

        <div v-for="post in posts" :key="post.id"
            style="border: 1px solid #ccc; padding: 15px; margin-bottom: 15px; border-radius: 8px;">
            <span style="background: #333; color: white; padding: 3px 8px; border-radius: 12px; font-size: 12px;">
                {{ post.category }}
            </span>
            <h2 style="margin: 10px 0 5px 0;">{{ post.title }}</h2>
            <p style="color: #666; font-size: 14px;">Oleh {{ post.author }} | {{ post.date_posted }}</p>
            <p>{{ post.content }}</p>

            <button v-if="authState.isLoggedIn && authState.username === post.author" @click="deletePost(post.id)"
                style="background: red; color: white; border: none; padding: 5px 10px; cursor: pointer; border-radius: 4px; margin-top: 10px;">
                Hapus Artikel
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import api from '../axios';
import { authState } from '../store';

const posts = ref([]);

const fetchPosts = async () => {
    try {
        const response = await api.get('/posts');
        posts.value = response.data.data;
    } catch (error) {
        console.error('Gagal menarik data artikel:', error);
    }
};

const deletePost = async (id) => {
    if (!confirm("Yakin ingin menghapus artikel ini?")) return;

    try {
        await api.delete(`/post/delete/${id}`);
        alert("Artikel berhasil dihapus");
        fetchPosts();
    } catch (error) {
        alert(error.response?.data?.error || "Gagal menghapus artikel");
    }
};

onMounted(fetchPosts);
</script>