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
      <li v-for="(item, index) in daftarKegiatan" :key="index" class="list-item">
        {{ item }}
        <button @click="hapusKegiatan(index)" class="hapus">Batalkan</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Input kegiatan baru
const kegiatanBaru = ref('')

// Daftar kegiatan
const daftarKegiatan = ref([])

// Tambah kegiatan ke daftar
function tambahKegiatan() {
  const teks = kegiatanBaru.value.trim()
  if (teks !== '') {
    daftarKegiatan.value.push(teks)
    kegiatanBaru.value = ''
  }
}

// Hapus kegiatan berdasarkan index
function hapusKegiatan(index) {
  daftarKegiatan.value.splice(index, 1)
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

.list-item {
  display: flex;
  justify-content: space-between;
  background: #f0f0f0;
  margin-bottom: 0.5rem;
  padding: 0.5rem;
  border-radius: 4px;
}

.hapus {
  background-color: #ff5c5c;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 0.3rem 0.7rem;
  cursor: pointer;
}

.hapus:hover {
  background-color: #d94a4a;
}
</style>
