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
    <p class="p1">Counter: {{ count }}</p>
    <button @click="increment">Tambah</button>
    
    <!-- Box Color Section -->
    <div :style="{ backgroundColor: boxColor, width: '200px', height: '200px', margin: '20px auto' }"></div>
    <button @click="changeColor">Ubah Warna Box</button>
    
    <!-- Image Carousel Section -->
    <div class="carousel">
      <img :src="images[currentImageIndex]" alt="carousel image" />
      <div class="carousel-buttons">
        <button class="prev" @click="prevImage">Previous</button>
        <button class="next" @click="nextImage">Next</button>
      </div>
    </div>
  </div>
</template>

<style>
div {
  margin: 0%;
  text-align: center;
  justify-content: center;
}

#app {
  display: block;
  grid-template-rows: none;
  grid-template-columns: none;
  gap: 0;
}

.p1 {
  padding-top: 20px;
  color: white;
  font-weight: medium;
  font-size: medium;
}

button {
  display: inline-block;
  color: white;
  background-color: rgb(0, 185, 0);
  padding: 10px 20px;
  text-decoration: none;
  border-radius: 15px;
  font-weight: medium;
  font-size: medium;
}

button:hover{
  background-color: rgb(0, 161, 0);
}

div > div {
  transition: background-color 0.3s ease;
}

.carousel {
  position: relative;
  text-align: center;
  width: 500px;
  margin-top: 10px;
}

.carousel img {
  margin: 20px auto;
  width: 100%;
  display: block;
  border-radius: 10px;
  transition: opacity 0.5s ease-in-out;
}

.carousel-buttons {
  width: 100%;
  bottom: 10px;
  display: flex;
  justify-content: space-between;
  padding: 0 20px 20px;
}

.prev, .next {
  background-color: rgb(0, 185, 0);
  color: white;
  padding: 10px 20px;
  border-radius: 15px;
  font-weight: medium;
  font-size: medium;
  border: none;
  cursor: pointer;
}

.prev:hover, .next:hover {
  background-color: rgb(0, 161, 0);
}
</style>
