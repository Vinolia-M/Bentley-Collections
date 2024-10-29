<template>
  <div class="navigation-bar">
    <h1 class="logo">BENTLEY</h1>
    <div class="products-x-humburger">
      <h3>ALL PRODUCTS</h3>
      <div class="humburger" @click="toggleMenu">
        <div class="line" :class="{ 'cross': isOpen }"></div>
        <div class="line" :class="{ 'cross': isOpen }"></div>
      </div>
    </div>
    <div v-if="isOpen" class="humburger-contents">
      <ul>
        <li>Bentley Batur Collections</li>
        <li>Bentley Bentayga Collections</li>
        <li>Bentley Continental GT Collections</li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import gsap from 'gsap';

const isOpen = ref(false);

const toggleMenu = () => {
  isOpen.value = !isOpen.value;

  if (isOpen.value) {

    gsap.to(".humburger-contents", {
      height: "100vh",
      opacity: 1,
      duration: 0.5,
      ease: "power2.inOut",
      onStart: () => {
        gsap.set(".humburger-contents", { display: "block", y: -20, opacity: 1 });
      },
    });
  } else {
  
    gsap.to(".humburger-contents", {
      height: 0,
      opacity: 0,
      duration: 0.5,
      ease: "power2.inOut",
      onComplete: () => {
        gsap.set(".humburger-contents", { display: "none" });
      },
    });
  }
};
</script>

<style scoped>
.navigation-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 30px 0;
  position: relative;
}

h1 {
  font-weight: 500;
  font-size: 25px;
}

h3 {
  font-size: 16px;
}

.products-x-humburger {
  display: flex;
  align-items: center;
  gap: 170px;
}

.humburger {
  position: relative;
  z-index: 1;
  display: grid;
  gap: 10px;
  cursor: pointer;
}

.line {
  background-color: #fff;
  min-width: 50px;
  height: 2px;
  transition: transform 0.3s ease;
}

.cross {
  background-color: #fff;
}

.cross:first-of-type {
  transform: rotate(45deg) translate(5px, 5px);
}

.cross:last-of-type {
  transform: rotate(-45deg) translate(5px, -5px);
}

.humburger-contents {
  position: absolute;
  top: 21%;
  left: -20%;
  right: -20%;
  min-height: 960px; 
  background-color: #002928;;
  padding: 0 20px; 
  overflow: hidden;
  opacity: 0; 
  transition: height 0.5s ease, opacity 0.5s ease;
  display: none; 
}

.humburger-contents ul {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  list-style-type: none;
  font-size: 30px;
}

.humburger-contents li {
  color: #fff;
}
</style>
