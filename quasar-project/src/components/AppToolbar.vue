<template>
  <q-toolbar class="floating-toolbar">
    <!-- Logo -->
    <div class="logo-section">
      <img src="../assets/SIBDC-LOGO.png" alt="SIBDC Logo" class="logo-image q-mr-sm" />
      <span class="logo-text">Synergy</span>
    </div>

    <!-- Desktop: Navigation tabs centered in the middle (width > 957px) -->
    <div class="nav-tabs-container" v-if="screenWidth > 957">
      <q-tabs v-model="activeTab" class="nav-tabs" indicator-color="transparent" active-color="#0A400C">
        <q-tab name="home" label="Home" @click="navigateTo('/')" />
        <q-tab name="about" label="About Us" @click="scrollToSection('about-us')" />
        <q-tab name="services" label="Services" @click="scrollToSection('services')" />
        <q-tab name="portfolio" label="Portfolio" @click="scrollToSection('portfolio')" />
        <q-tab name="story" label="Our Story" @click="navigateTo('/story')" />
      </q-tabs>
    </div>

    <!-- Mobile: Empty spacer (width <= 957px) -->
    <div v-if="screenWidth <= 957" class="q-space"></div>

    <!-- Mobile: Hamburger menu (width <= 957px) -->
    <div v-if="screenWidth <= 957" class="mobile-menu">
      <q-btn
        flat
        icon="menu"
        class="mobile-menu-btn"
        ripple
      >
        <q-menu class="mobile-menu-list" anchor="bottom right" self="top right">
          <q-list>
            <q-item clickable v-close-popup @click="navigateToHome">
              <q-item-section>Home</q-item-section>
            </q-item>
            <q-item clickable v-close-popup @click="scrollToSection('about-us')">
              <q-item-section>About Us</q-item-section>
            </q-item>
            <q-item clickable v-close-popup @click="scrollToSection('services')">
              <q-item-section>Services</q-item-section>
            </q-item>
            <q-item clickable v-close-popup @click="scrollToSection('portfolio')">
              <q-item-section>Portfolio</q-item-section>
            </q-item>
            <q-item clickable v-close-popup>
              <q-item-section>Our Story</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup @click="navigateToContact">
              <q-item-section avatar>
                <q-icon name="email" color="#0A400C" />
              </q-item-section>
              <q-item-section style="color: #0A400C; font-weight: 600; white-space: nowrap;">Contact Us</q-item-section>
            </q-item>
          </q-list>
        </q-menu>
      </q-btn>
    </div>

    <!-- Desktop: Contact Us button -->
    <div v-if="screenWidth > 957" class="contact-btn-section">
      <q-btn
        style="background: #0A400C; color: #FEFAE0;"
        label="Contact Us"
        no-caps
        class="contact-btn"
        icon="email"
        @click="navigateToContact"
      />
    </div>
  </q-toolbar>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const activeTab = ref('home')
const screenWidth = ref(window.innerWidth)

function navigateTo(route) {
  router.push(route)
}

function scrollToSection(sectionId) {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth', block: 'start' })
  }
}

function navigateToHome() {
  router.push('/')
  // Scroll to top when navigating to home
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function navigateToContact() {
  console.log('Navigate to contact page')
}

function updateScreenWidth() {
  screenWidth.value = window.innerWidth
}

onMounted(() => {
  window.addEventListener('resize', updateScreenWidth)
})

onUnmounted(() => {
  window.removeEventListener('resize', updateScreenWidth)
})
</script>

<style scoped>
.floating-toolbar {
  background: rgba(254, 250, 224, 0.95);
  backdrop-filter: blur(10px);
  border-radius: 25px;
  min-height: 60px;
  padding: 0 32px;
  margin: 12px auto;
  width: calc(100vw - 48px);
  max-width: 1200px;
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

.logo-image {
  height: 32px;
  width: auto;
  object-fit: contain;
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
  margin: 0 10px;
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

.mobile-menu {
  margin-right: 0px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 60px;
}

.mobile-menu-btn {
  color: #0A400C;
  font-size: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 40px;
  min-width: 40px;
}

.mobile-menu-btn:focus,
.mobile-menu-btn:active,
.mobile-menu-btn.q-btn--active {
  box-shadow: none !important;
  background: none !important;
}



.mobile-menu-list {
  background: rgba(254, 250, 224, 0.98);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  border: 1px solid rgba(177, 171, 134, 0.3);
  box-shadow: 0 8px 32px rgba(10, 64, 12, 0.15);
  min-width: 160px;
  margin-top: 8px;
  margin-right: -8px;
}

.mobile-menu-list .q-item {
  color: #819067;
  font-weight: 500;
  padding: 12px 16px;
  border-radius: 8px;
  margin: 4px;
  transition: all 0.2s ease;
}

.mobile-menu-list .q-item:hover {
  background: rgba(129, 144, 103, 0.15);
  color: #0A400C;
}

.contact-btn-section {
  display: flex;
  align-items: center;
}

.contact-btn {
  font-weight: 600;
  border-radius: 20px;
  padding: 8px 20px;
  transition: all 0.3s ease;
  box-shadow: 0 2px 8px rgba(10, 64, 12, 0.2);
}

.contact-btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(10, 64, 12, 0.3);
  background: #819067 !important;
}

@media (max-width: 956px) {
  .floating-toolbar {
    margin: 8px 12px;
    padding: 0 20px;
    min-height: 60px;
    width: calc(100vw - 24px);
    max-width: calc(100vw - 24px);
  }

  .mobile-menu-btn {
    min-height: 40px;
    min-width: 40px;
    font-size: 24px;
  }


  .logo-text {
    font-size: 20px;
  }
}
</style>
