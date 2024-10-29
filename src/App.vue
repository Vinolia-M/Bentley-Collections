<template>
  <header>
    <div class="wrapper">
      <Navigation />
    </div>
  </header>

  <main>
    <Body />
  </main>
  
  <footer>
    <TheFooter />
  </footer>
</template>

<script setup lang="ts">
  import Navigation from './components/Navigation.vue'
  import TheFooter from './components/TheFooter.vue'
  import Body from './components/Body.vue'
</script>