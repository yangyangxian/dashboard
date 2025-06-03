<template>
  <v-layout class="rounded rounded-md border layout">
    <v-navigation-drawer id="navigation-drawer" width="200">
      <v-list nav v-model="selectedItem">
        <v-list-item
          value="/dashboards/todo-reminder"
          active-class="bg-primary"
          :active="selectedItem === '/dashboards/todo-reminder'"
          to="/dashboards/todo-reminder"
        >
          <v-list-item-title class="navigation-item-title">To do reminder</v-list-item-title>
        </v-list-item>
        <v-list-item
          value="/dashboards/portal-one"
          active-class="bg-primary"
          :active="selectedItem === '/dashboards/portal-one'"
          to="/dashboards/portal-one"
        >
          <v-list-item-title class="navigation-item-title">Portal One</v-list-item-title>
        </v-list-item>
        <v-list-item
          value="/dashboards/dashboard-page"
          active-class="bg-primary"
          :active="selectedItem === '/dashboards/dashboard-page'"
          to="/dashboards/dashboard-page"
        >
          <v-list-item-title class="navigation-item-title">Dashboard</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar title="Application bar">
      <template v-slot:append>
        <v-btn
          :icon="theme.global.current.value.dark ? 'mdi-weather-sunny' : 'mdi-weather-night'"
          @click="toggleTheme"
        ></v-btn>
      </template>
    </v-app-bar>

    <v-main class="d-flex justify-center">
      <v-container>
        <router-view />
      </v-container>
    </v-main>
  </v-layout>
</template>

<script setup lang="ts">
  import { ref, watchEffect } from 'vue'
  import { useRoute } from 'vue-router'
  import { useTheme } from 'vuetify'

  const route = useRoute()
  const selectedItem = ref(route.path)

  watchEffect(() => {
    selectedItem.value = route.path
  })

  const theme = useTheme()

  function toggleTheme () {
    theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
  }
</script>

<style scoped>
#navigation-drawer :deep(.navigation-item-title) {
  font-size: 1rem;
}

.layout {
  height: calc(100vh - 40px); /* 40px is the height of the footer bar */
}
</style>
