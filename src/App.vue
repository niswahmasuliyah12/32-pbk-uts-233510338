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
      <button type="submit">
        <i class="fa fa-plus"></i> Tambah
      </button>
    </form>

    <!-- Filter checkbox -->
    <div class="filter">
      <label>
        <input type="checkbox" v-model="tampilkanBelumSelesai" />
        <i class="fa fa-filter"></i> Tampilkan hanya yang belum selesai
      </label>
    </div>

    <!-- Daftar kegiatan -->
    <ul class="list">
      <li
        v-for="(item, index) in kegiatanTersaring"
        :key="index"
        class="list-item"
        :class="{ selesai: item.selesai }"
      >
        <label>
          <input type="checkbox" v-model="item.selesai" />
          <span>{{ item.nama }}</span>
        </label>
        <button @click="hapusKegiatan(index)" class="hapus">
          <i class="fa fa-trash"></i> Batalkan
        </button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// Input kegiatan baru
const kegiatanBaru = ref('')

// Daftar kegiatan
const daftarKegiatan = ref([])

// Filter: hanya tampilkan yang belum selesai
const tampilkanBelumSelesai = ref(false)

// Computed: kegiatan yang sesuai filter
const kegiatanTersaring = computed(() => {
  return tampilkanBelumSelesai.value
    ? daftarKegiatan.value.filter(item => !item.selesai)
    : daftarKegiatan.value
})

// Tambah kegiatan
function tambahKegiatan() {
  const teks = kegiatanBaru.value.trim()
  if (teks !== '') {
    daftarKegiatan.value.push({ nama: teks, selesai: false })
    kegiatanBaru.value = ''
  }
}

// Hapus kegiatan
function hapusKegiatan(index) {
  daftarKegiatan.value.splice(index, 1)
}
</script>

<style scoped>
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #f7f9fc;
  font-family: 'Arial', sans-serif;
}

.container {
  max-width: 600px;
  margin: 3rem auto;
  padding: 2.5rem;
  background: linear-gradient(135deg, #6a11cb, #2575fc);
  border-radius: 12px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
  animation: fadeIn 1s ease-in-out;
}

h1 {
  text-align: center;
  color: #fff;
  margin-bottom: 2rem;
  font-size: 2rem;
  text-transform: uppercase;
  letter-spacing: 1.5px;
}

.form {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
  transition: transform 0.3s ease;
}

input[type="text"] {
  flex: 1;
  padding: 0.8rem;
  font-size: 1.1rem;
  border: 2px solid #ddd;
  border-radius: 8px;
  transition: border-color 0.3s ease, transform 0.3s ease;
}

input[type="text"]:focus {
  border-color: #2575fc;
  outline: none;
  transform: scale(1.05);
}

button {
  padding: 0.8rem 1.5rem;
  font-size: 1.1rem;
  background-color: #2575fc;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

button i {
  font-size: 1.2rem;
}

button:hover {
  background-color: #1e56a0;
  transform: scale(1.05);
}

.filter {
  margin-bottom: 1.5rem;
  text-align: center;
  font-size: 1rem;
  color: #fff;
  animation: slideIn 0.5s ease-out;
}

.filter input[type="checkbox"] {
  margin-right: 0.5rem;
  accent-color: #2575fc;
}

.list {
  list-style: none;
  padding: 0;
  margin-top: 2rem;
  animation: fadeInUp 0.7s ease-out;
}

.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #fff;
  margin-bottom: 1rem;
  padding: 1rem 1.2rem;
  border-radius: 8px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, background-color 0.3s ease;
}

.list-item:hover {
  background-color: #f2f8ff;
  transform: translateY(-5px);
}

.list-item label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}

.list-item input[type="checkbox"] {
  accent-color: #2575fc;
  width: 20px;
  height: 20px;
}

.list-item.selesai span {
  text-decoration: line-through;
  color: #aaa;
  opacity: 0.7;
}

.hapus {
  background-color: #ff4747;
  color: white;
  border: none;
  border-radius: 6px;
  padding: 0.5rem 1rem;
  font-size: 0.95rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.hapus i {
  font-size: 1rem;
}

.hapus:hover {
  background-color: #d13c3c;
  transform: scale(1.05);
}

/* Animations */
@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideIn {
  0% {
    opacity: 0;
    transform: translateX(-100%);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInUp {
  0% {
    opacity: 0;
    transform: translateY(30px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
