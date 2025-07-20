<template>
  <q-layout view="lHh LpR lFf">
    <!-- Header with responsive navigation -->
    <q-header class="bg-white text-dark" style="box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
      <q-toolbar class="coffee-mobile-toolbar">
        <!-- Mobile: Menu button -->
        <q-btn
          v-if="$q.screen.lt.lg"
          flat
          dense
          round
          icon="menu"
          color="dark"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <!-- Logo/Title with icon -->
        <div class="logo-section cursor-pointer" @click="$router.push('/')">
          <q-icon name="favorite" color="orange" size="md" class="q-mr-sm" />
          <span class="logo-text">Synergy</span>
        </div>

        <q-space />

        <!-- Desktop: Navigation tabs only -->
        <q-tabs
          v-if="$q.screen.gt.md"
          v-model="activeTab"
          class="text-dark desktop-tabs"
          active-color="orange"
          indicator-color="orange"
          align="center"
          shrink
          stretch
        >
          <q-tab
            v-for="item in navigationItems"
            :key="item.name"
            :name="item.name"
            :label="item.label"
            @click="navigateTo(item.route)"
            no-caps
            class="tab-item"
          />
        </q-tabs>

        <q-space />

        <!-- Mobile: User avatar -->
        <q-btn v-if="$q.screen.lt.lg" flat round dense>
          <q-avatar size="32px">
            <img src="https://cdn.quasar.dev/img/avatar2.jpg">
          </q-avatar>
        </q-btn>
      </q-toolbar>
    </q-header>

    <!-- Mobile: Left drawer navigation -->
    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :breakpoint="1024"
      bordered
      class="bg-grey-1"
      :width="280"
    >
      <q-scroll-area class="fit">
        <!-- User info section -->
        <div class="q-pa-md bg-orange text-white">
          <div class="row items-center q-gutter-md">
            <q-avatar size="48px">
              <q-icon name="favorite" color="white" size="lg" />
            </q-avatar>
            <div>
              <div class="text-weight-bold">Synergy</div>
              <div class="text-caption opacity-70">Welcome to Synergy</div>
            </div>
          </div>
        </div>

        <!-- Navigation items -->
        <q-list padding>
          <q-item
            v-for="item in navigationItems"
            :key="item.name"
            clickable
            v-ripple
            :active="activeTab === item.name"
            active-class="text-orange bg-orange-1"
            @click="navigateTo(item.route)"
          >
            <q-item-section avatar>
              <q-icon :name="item.icon" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ item.label }}</q-item-label>
              <q-item-label caption v-if="item.description">
                {{ item.description }}
              </q-item-label>
            </q-item-section>
          </q-item>

          <q-separator class="q-my-md" />

          <!-- Mobile login options -->
          <q-item clickable v-ripple @click="customerLogin">
            <q-item-section avatar>
              <q-icon name="person" />
            </q-item-section>
            <q-item-section>
              <q-item-label>Customer Login</q-item-label>
            </q-item-section>
          </q-item>

          <q-item clickable v-ripple @click="partnerLogin">
            <q-item-section avatar>
              <q-icon name="business" />
            </q-item-section>
            <q-item-section>
              <q-item-label>Partner Login</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import { useQuasar } from 'quasar'

const $q = useQuasar()
const router = useRouter()
const route = useRoute()

const leftDrawerOpen = ref(false)
const activeTab = ref('home')

const navigationItems = [
  {
    name: 'home',
    label: 'Home',
    icon: 'home',
    route: '/',
    description: 'Landing page'
  },
  {
    name: 'about',
    label: 'About Us',
    icon: 'info',
    route: '/about',
    description: 'Learn about us'
  },
  {
    name: 'portfolio',
    label: 'Portfolio',
    icon: 'work',
    route: '/portfolio',
    description: 'Our work showcase'
  },
  {
    name: 'services',
    label: 'Services',
    icon: 'build',
    route: '/services',
    description: 'What we offer'
  },
  {
    name: 'story',
    label: 'Our Story',
    icon: 'auto_stories',
    route: '/story',
    description: 'Our journey'
  }
]

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

function navigateTo(route) {
  router.push(route)
  // Close drawer on mobile after navigation
  if ($q.screen.lt.lg) {
    leftDrawerOpen.value = false
  }
}

function customerLogin() {
  // Handle customer login
  console.log('Customer login clicked')
}

function partnerLogin() {
  // Handle partner login
  console.log('Partner login clicked')
}

// Update active tab based on current route
const updateActiveTab = () => {
  const currentPath = route.path
  const matchedItem = navigationItems.find(item => item.route === currentPath)
  if (matchedItem) {
    activeTab.value = matchedItem.name
  }
}

// Watch for route changes
router.afterEach(() => {
  updateActiveTab()
})

// Initialize active tab
updateActiveTab()
</script>

<style lang="scss" scoped>
.coffee-mobile-toolbar {
  min-height: 70px;
  padding: 0 24px;

  @media (max-width: 1023px) {
    padding: 0 16px;
  }
}

.logo-section {
  display: flex;
  align-items: center;

  .logo-text {
    font-size: 24px;
    font-weight: 700;
    color: #8B4513;
    font-family: 'Roboto', sans-serif;
  }
}

.desktop-tabs {
  flex: 1;
  max-width: 600px;

  .tab-item {
    font-size: 16px;
    font-weight: 500;
    color: #666;
    padding: 12px 24px;
    transition: all 0.2s ease;

    &:hover {
      color: #333;
      background-color: rgba(0,0,0,0.04);
    }
  }
}

.q-drawer {
  .q-item {
    border-radius: 8px;
    margin: 2px 8px;
  }
}

// Mobile adjustments
@media (max-width: 1023px) {
  .logo-section .logo-text {
    font-size: 20px;
  }
}
</style>
