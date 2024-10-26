<script setup>


import Header from './components/Header.vue'
import Hero from './components/Hero.vue';
import HomeCards from './components/HomeCards.vue';
import JobListings from './components/JobListings.vue';


</script>

<template>
  <Header />
  <Hero />
  <HomeCards />
  <JobListings :limitPost="3" :showButton="true" />
</template>


<style scoped></style>
