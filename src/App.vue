<script setup>
import { ref } from 'vue'; // Import ref untuk reactive data

// Impor gambar lokal dari folder assets
import image1 from '@/assets/image1.jpg';
import image2 from '@/assets/image2.jpg';
import image3 from '@/assets/image3.jpg';

const count = ref(0); // Inisialisasi counter
const boxColor = ref('red'); // Inisialisasi warna box
const currentImageIndex = ref(0); // Inisialisasi index gambar yang tampil saat ini

// Daftar gambar lokal untuk carousel
const images = [image1, image2, image3];

const colors = ['red', 'magenta', 'blue', 'cyan', 'green', 'yellow']; // Daftar warna
let colorIndex = 0; // Indeks warna saat ini

function increment() {
  count.value++; // Fungsi untuk menambah counter
}

function changeColor() {
  // Mengubah warna kotak sesuai urutan yang ada di array
  boxColor.value = colors[colorIndex];
  colorIndex = (colorIndex + 1) % colors.length; // Perbarui indeks warna
}

function nextImage() {
  currentImageIndex.value = (currentImageIndex.value + 1) % images.length; // Pindah ke gambar berikutnya
}

function prevImage() {
  currentImageIndex.value = (currentImageIndex.value - 1 + images.length) % images.length; // Pindah ke gambar sebelumnya
}
</script>

<template>
  <div>
    <!-- Counter Section -->
    <p>Counter: {{ count }}</p>
    <button @click="increment">Tambah</button>
    
    <!-- Box Color Section -->
    <div :style="{ backgroundColor: boxColor, width: '200px', height: '200px', margin: '20px auto' }"></div>
    <button @click="changeColor">Ubah Warna Box</button>
    
    <!-- Image Carousel Section -->
    <div class="carousel">
      <img :src="images[currentImageIndex]" alt="carousel image" />
      <div>
        <button @click="prevImage">Previous</button>
        <button @click="nextImage">Next</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
div {
  text-align: center;
  margin-top: 2rem;
}

button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  cursor: pointer;
  color: white;
  background-color: rgb(0, 185, 0);
  border-radius: 10%;
}

div > div {
  transition: background-color 0.3s ease;
}

.carousel {
  text-align: center;
  width: 500px;
  margin-top: 10;
}

.carousel img {
  width: 100%;
  display: block;
  border-radius: 10px;
  transition: opacity 0.5s ease-in-out;
}
</style>
