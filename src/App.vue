<template>
  <div class="container">
    <h1>Daftar Kegiatan</h1>

    <!-- Form input kegiatan -->
    <form @submit.prevent="tambahKegiatan" class="form">
      <input
        v-model="kegiatanBaru"
        type="text"
        placeholder="Masukkan kegiatan baru"
        required
      />
      <button type="submit">Tambah</button>
    </form>

    <!-- Daftar kegiatan -->
    <ul class="list">
      <li v-for="(item, index) in daftarKegiatan" :key="index">
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Input kegiatan baru
const kegiatanBaru = ref('')

// Array untuk menyimpan daftar kegiatan
const daftarKegiatan = ref([])

// Fungsi menambahkan kegiatan ke daftar
function tambahKegiatan() {
  const teks = kegiatanBaru.value.trim()
  if (teks !== '') {
    daftarKegiatan.value.push(teks)
    kegiatanBaru.value = '' // Reset input setelah ditambahkan
  }
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 1rem;
  font-family: Arial, sans-serif;
}

.form {
  display: flex;
  gap: 0.5rem;
}

input {
  flex: 1;
  padding: 0.5rem;
  font-size: 1rem;
}

button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #369870;
}

.list {
  margin-top: 1rem;
  list-style: none;
  padding: 0;
}

li {
  background: #f0f0f0;
  margin-bottom: 0.5rem;
  padding: 0.5rem;
  border-radius: 4px;
}
</style>
