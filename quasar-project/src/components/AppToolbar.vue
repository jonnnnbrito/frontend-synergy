<template>
  <q-toolbar class="floating-toolbar">
    <!-- Logo -->
    <div class="logo-section">
      <q-icon name="favorite" size="md" class="q-mr-sm" style="color: #0A400C;" />
      <span class="logo-text">Synergy</span>
    </div>

    <!-- Navigation tabs centered in the middle -->
    <div class="nav-tabs-container">
      <q-tabs v-model="activeTab" class="nav-tabs" indicator-color="transparent" active-color="#0A400C">
        <q-tab name="home" label="Home" />
        <q-tab name="about" label="About Us" />
        <q-tab name="portfolio" label="Portfolio" />
        <q-tab name="services" label="Services" />
        <q-tab name="story" label="Our Story" />
      </q-tabs>
    </div>

    <!-- Right side spacer (same width as logo section for perfect centering) -->
    <div class="logo-section" style="visibility: hidden;">
      <q-icon name="favorite" size="md" class="q-mr-sm" style="color: #0A400C;" />
      <span class="logo-text">Synergy</span>
    </div>
  </q-toolbar>
</template>

<script setup>
import { ref } from 'vue'
const activeTab = ref('home')
</script>

<style scoped>
.floating-toolbar {
  background: rgba(254, 250, 224, 0.95);
  backdrop-filter: blur(10px);
  border-radius: 25px;
  min-height: 60px;
  padding: 0 32px;
  margin: 12px 24px;
  width: calc(100vw - 48px);
  max-width: calc(100vw - 48px);
  box-shadow: 0 8px 32px rgba(10, 64, 12, 0.15);
  border: 1px solid rgba(177, 171, 134, 0.3);
  transition: all 0.3s ease;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.floating-toolbar:hover {
  box-shadow: 0 12px 40px rgba(10, 64, 12, 0.2);
}

.logo-section {
  display: flex;
  align-items: center;
}

.logo-text {
  font-size: 22px;
  font-weight: 700;
  color: #0A400C;
  font-family: 'Roboto', sans-serif;
}

.nav-tabs-container {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.nav-tabs {
  color: #666;
  border-radius: 15px;
  flex: 0 0 auto;
}

.nav-tabs .q-tabs__content {
  justify-content: center !important;
}

.nav-tabs .q-tab {
  color: #819067;
  font-weight: 500;
  border-radius: 12px;
  margin: 0 4px;
  transition: all 0.2s ease;
}

.nav-tabs .q-tab:hover {
  background: rgba(129, 144, 103, 0.15);
  color: #0A400C;
}

.nav-tabs .q-tab--active {
  background: rgba(10, 64, 12, 0.1);
  color: #0A400C;
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
