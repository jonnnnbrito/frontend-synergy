<template>
  <q-layout view="lHh LpR lFf">
    <!-- Floating Toolbar -->
    <div class="floating-toolbar-container">
      <AppToolbar @toggle-drawer="toggleLeftDrawer" />
    </div>

    <!-- Page content -->
    <q-page-container class="main-content">
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
.floating-toolbar-container {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 2000;
  pointer-events: none;
}

.floating-toolbar-container > * {
  pointer-events: auto;
}

.main-content {
  padding-top: 0;
}

.q-drawer {
  .q-item {
    border-radius: 8px;
    margin: 2px 8px;
  }
}
</style>
