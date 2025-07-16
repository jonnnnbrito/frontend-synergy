<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-primary">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
          class="lg:hidden"
        />

        <q-toolbar-title class="text-h5 text-weight-bold">
          Synergy
        </q-toolbar-title>

        <q-space />

        <div class="hidden lg:flex q-gutter-lg">
          <q-btn flat label="Home" @click="scrollToSection('home')" />
          <q-btn flat label="About" @click="scrollToSection('about')" />
          <q-btn flat label="Services" @click="scrollToSection('services')" />
          <q-btn flat label="Team" @click="scrollToSection('team')" />
          <q-btn flat label="Contact" @click="scrollToSection('contact')" />
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="lg:hidden"
    >
      <q-list>
        <q-item-label header class="text-grey-8">
          Navigation
        </q-item-label>

        <q-item 
          v-for="link in navigationLinks"
          :key="link.title"
          clickable
          @click="scrollToSection(link.section)"
          class="text-grey-7"
        >
          <q-item-section avatar>
            <q-icon :name="link.icon" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{ link.title }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'

const navigationLinks = [
  {
    title: 'Home',
    section: 'home',
    icon: 'home'
  },
  {
    title: 'About',
    section: 'about',
    icon: 'info'
  },
  {
    title: 'Services',
    section: 'services',
    icon: 'work'
  },
  {
    title: 'Team',
    section: 'team',
    icon: 'group'
  },
  {
    title: 'Contact',
    section: 'contact',
    icon: 'contact_mail'
  }
]

const leftDrawerOpen = ref(false)

function toggleLeftDrawer () {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

function scrollToSection(section) {
  const element = document.getElementById(section)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
  leftDrawerOpen.value = false
}
</script>
