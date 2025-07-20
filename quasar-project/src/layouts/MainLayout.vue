<template>
  <q-layout view="lHh LpR lFf">
    <!-- Header with responsive navigation -->
    <q-header class="bg-white text-dark" style="box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
      <AppToolbar @toggle-drawer="toggleLeftDrawer" />
    </q-header>

    <!-- Mobile: Left drawer navigation -->
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import AppToolbar from 'src/components/AppToolbar.vue'

const leftDrawerOpen = ref(false)

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}
</script>

<style lang="scss" scoped>
.q-drawer {
  .q-item {
    border-radius: 8px;
    margin: 2px 8px;
  }
}
</style>
