<script setup lang="ts">
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import Image1 from '@/assets/yellow-bentley.jpg';
import Image2 from '@/assets/bentley-bacalar.jpg';
import Image3 from '@/assets/bentley-mulliner-batur.jpg';
import Image4 from '@/assets/batur.jpg';
import Image5 from '@/assets/bentley-logo.jpg';

const backgroundImages = [Image1, Image2, Image3, Image4, Image5];

const content = [
  { title: 'EXPERIENCE', heading: 'TURBO<br/>SENSATION', text: 'Discover the essence of luxury driving with Bentley. Experience unmatched craftsmanship and style, where every journey becomes an extraordinary adventure, elevating your status on the road.' },
  { title: 'IGNITE', heading: 'HIGH<br/>HORSEPOWER', text: 'Step into a world of unrivaled luxury with Bentley. Each vehicle is a testament to precision engineering, ensuring a smooth, powerful ride wrapped in comfort.' },
  { title: 'CRUISE IN', heading: 'ROAD RUSH', text: 'Embark on a unique journey with Bentley, where timeless elegance meets cutting-edge technology. Revel in opulence and power, making every drive a true masterpiece.' },
  { title: 'GEAR UP', heading: 'ADRENELINE<br/>DRIVE', text: 'Experience the perfect fusion of luxury and performance with Bentley. Every drive transforms into an unforgettable journey, showcasing exquisite craftsmanship and unparalleled sophistication at every turn.' },
  { title: 'FIRE UP', heading: 'ACCELERATE', text: 'Experience the perfect fusion of luxury and performance with Bentley. Every drive transforms into an unforgettable journey, showcasing exquisite craftsmanship and unparalleled sophistication at every turn.' } 
];

const titleColors = ['#FF5733', '#33FF57', '#3357FF', '#F0FF33', 'rgb(255 0 0)']; 
const currentIndex = ref(0);

const previousBackground = () => {
  const newIndex = currentIndex.value > 0 ? currentIndex.value - 1 : backgroundImages.length - 1;
  changeBackground(newIndex);
};

const nextBackground = () => {
  const newIndex = (currentIndex.value + 1) % backgroundImages.length;
  changeBackground(newIndex);
};

const changeBackground = (index: number) => {
  gsap.to('.body-content', {
    opacity: 0,
    duration: 0.5,
    onComplete: () => {
      currentIndex.value = index;
      gsap.to('.body-content', { opacity: 1, duration: 0.5 });
    }
  });
};

const getDotColor = (index: number) => {
  return index === currentIndex.value ? '#FFFFFF' : '#808080';
};

onMounted(() => {
  gsap.set('.body-content', { opacity: 1 });
});
</script>

<template>
  <div class="body-content" :style="{ backgroundImage: `url(${backgroundImages[currentIndex]})` }">
    <div class="content">
      <div class="inner-contents">
        <h2 :style="{ color: titleColors[currentIndex] }">{{ content[currentIndex].title }}</h2>
        <h1 v-html="content[currentIndex].heading"></h1>
        <button class="cruis-in">CRUIS IN</button>
      </div>
      <div class="right-content">
        <span class="dot">{{ currentIndex + 1 }}</span>
        <p>{{ content[currentIndex].text }}</p>
      </div>
    </div>

    <div class="navigation-buttons">
      <button @click="previousBackground" class="nav-button prev-button">
        <img src="./icons/left-arrow.svg" alt="Previous" class="arrow-icon" />
      </button>
      <div class="dots-container">
        <span 
          v-for="(dot, index) in backgroundImages.length" 
          :key="index" 
          class="dots" 
          :style="{ backgroundColor: getDotColor(index) }">
        </span>
      </div>
      <button @click="nextBackground" class="nav-button next-button">
        <img src="./icons/right-arrow.svg" alt="Next" class="arrow-icon" />
      </button>
    </div>
  </div>
</template>

<style scoped>
.body-content {
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
  height: 100%;
  background-size: cover;
  background-position: center;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  transition: background-image 0.5s ease-in-out;
}

.content {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 200px;
  margin: 0 120px;
  padding: 0 2rem;
}

.inner-contents {
  width: 50%;
}

.right-content {
  font-size: 20px;
  width: 50%;
}

h1 {
  font-weight: 600;
  font-style: italic;
  font-size: 90px;
  line-height: 0.8;
  margin-bottom: 30px;
  margin-left: -11px;
}

h2 {
  font-weight: 600;
  font-style: italic;
  font-size: 25px;
  margin-bottom: 5px;
}

.cruis-in {
  background: transparent;
  border-radius: 30px;
  border: 1px solid #fff;
  padding: 11px 30px;
  color: #fff;
  font-weight: 600;
  font-size: 17px;
  cursor: pointer;
}

.cruis-in:hover {
  scale: 1.2;
  transition: all 0.5s ease-in-out;
}

.navigation-buttons {
  position: absolute;
  bottom: 40px;
  left: 8%;
  display: flex;
  align-items: center;
  gap: 17px;
  margin-top: 20px;
}

.nav-button {
  background: transparent;
  border: none;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 16px;
  cursor: pointer;
  position: relative;
  transition: background-color 0.3s;
}

.dots-container {
  display: flex;
  gap: 10px;
}

.dot {
    border: 1px solid #fff;
    border-radius: 50%;
    aspect-ratio: 1/1;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 60px;
    font-size: 40px;
    margin-bottom: 20px;
}

.dots {
  border-radius: 50%;
  height: 8px;
  width: 8px;
  background: #808080; 
}

@media screen and (max-width:1024px) {
  .content {
    flex-direction: column;
    gap: 55px;
}

.inner-contents {width: 100%;}
.right-content {width: 100%;}
}
</style>
