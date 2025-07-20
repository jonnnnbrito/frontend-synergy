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
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  border-radius: 25px;
  min-height: 60px;
  padding: 0 32px;
  margin: 12px 24px;
  width: calc(100vw - 48px);
  max-width: calc(100vw - 48px);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.3s ease;
}

.floating-toolbar:hover {
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
  transform: translateY(-2px);
}

.logo-section {
  display: flex;
  align-items: center;
}

.logo-text {
  font-size: 22px;
  font-weight: 700;
  color: #8B4513;
  font-family: 'Roboto', sans-serif;
}

.nav-tabs {
  color: #666;
  border-radius: 15px;
}

.nav-tabs .q-tab {
  color: #666;
  font-weight: 500;
  border-radius: 12px;
  margin: 0 4px;
  transition: all 0.2s ease;
}

.nav-tabs .q-tab:hover {
  background: rgba(255, 165, 0, 0.1);
  color: #333;
}

.nav-tabs .q-tab--active {
  background: rgba(255, 165, 0, 0.2);
  color: #ff6600;
}

@media (max-width: 768px) {
  .floating-toolbar {
    margin: 8px 12px;
    padding: 0 16px;
    min-height: 50px;
    width: calc(100vw - 24px);
    max-width: calc(100vw - 24px);
  }
  
  .logo-text {
    font-size: 18px;
  }
}
</style>
