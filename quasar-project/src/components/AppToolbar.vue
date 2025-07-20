<template>
  <q-toolbar class="floating-toolbar">
    <!-- Logo -->
    <div class="logo-section">
      <q-icon name="favorite" color="orange" size="md" class="q-mr-sm" />
      <span class="logo-text">Synergy</span>
    </div>

    <q-space />

    <!-- Navigation tabs -->
    <q-tabs v-model="activeTab" class="nav-tabs">
      <q-tab name="home" label="Home" />
      <q-tab name="about" label="About Us" />
      <q-tab name="portfolio" label="Portfolio" />
      <q-tab name="services" label="Services" />
      <q-tab name="story" label="Our Story" />
    </q-tabs>

    <q-space />
  </q-toolbar>
</template>

<script setup>
import { ref } from 'vue'
const activeTab = ref('home')
</script>

<style scoped>
.floating-toolbar {
  margin: 0px;
  padding: 0 24px;
  background: transparent;
  border-radius: 20px;
  min-height: 70px;
}

.logo-text {
  font-size: 24px;
  font-weight: 700;
  color: #8B4513;
}

.nav-tabs {
  color: #666;
}
</style>
