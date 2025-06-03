<template>
  <v-layout class="rounded rounded-md border h-screen">
    <v-navigation-drawer width="200">
      <v-list nav v-model="selectedItem">
        <v-list-item
          title="To do reminder"
          value="todo-reminder"
          active-class="bg-primary"
          :active="selectedItem === 'todo-reminder'"
          @click="activeComponent = TodoReminder; selectedItem = 'todo-reminder'"
        ></v-list-item>
        <v-list-item
          title="Portal One"
          value="portal-one"
          active-class="bg-primary"
          :active="selectedItem === 'portal-one'"
          @click="activeComponent = PortalOne; selectedItem = 'portal-one'"
        ></v-list-item>
        <v-list-item
          title="Dashboard"
          value="dashboard-page"
          active-class="bg-primary"
          :active="selectedItem === 'dashboard-page'"
          @click="activeComponent = DashboardPage; selectedItem = 'dashboard-page'"
        ></v-list-item>
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
        <component :is="activeComponent" />
      </v-container>
    </v-main>
  </v-layout>
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  import { useTheme } from 'vuetify'

  import DashboardPage from './dashboard-page.vue'
  import PortalOne from './portal-one.vue'
  import TodoReminder from './todo-reminder.vue'

  const activeComponent = ref(TodoReminder)
  const selectedItem = ref('todo-reminder')

  const theme = useTheme()

  function toggleTheme () {
    theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
  }
</script>