<template>
    <div style="padding: 20px;">
        <h2>Tulis Artikel Baru</h2>
        <form @submit.prevent="submitPost">
            <div style="margin-bottom: 10px;">
                <label>Judul:</label><br>
                <input v-model="title" type="text" required style="width: 100%; max-width: 400px; padding: 5px;" />
            </div>

            <div style="margin-bottom: 10px;">
                <label>Kategori:</label><br>
                <input v-model="category" type="text" placeholder="Contoh: Tutorial, Teknologi" required
                    style="width: 100%; max-width: 400px; padding: 5px;" />
            </div>

            <div style="margin-bottom: 15px;">
                <label>Konten:</label><br>
                <textarea v-model="content" rows="8" required
                    style="width: 100%; max-width: 400px; padding: 5px;"></textarea>
            </div>

            <button type="submit"
                style="padding: 8px 15px; background: #28a745; color: white; border: none; border-radius: 4px; cursor: pointer;">
                Terbitkan Artikel
            </button>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import api from '../axios';

const title = ref('');
const category = ref('');
const content = ref('');
const router = useRouter();

const submitPost = async () => {
    try {
        await api.post('/post/create', {
            title: title.value,
            category: category.value,
            content: content.value
        });

        alert('Artikel berhasil diterbitkan!');
        router.push('/');
    } catch (error) {
        alert(error.response?.data?.error || 'Gagal menerbitkan artikel. Pastikan Anda sudah login.');
    }
};
</script>