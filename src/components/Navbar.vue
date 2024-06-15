<!-- Navbar.vue -->
<template>
    <q-toolbar class="bg text-white">
      <q-toolbar-title>Projects</q-toolbar-title>
      <q-btn-dropdown
        flat
        label="Tugas"
        color="white"
        text-color="white"
        size="18px"
        dense
      >
        <q-list style="min-width: 160px">
          <q-item v-for="task in tasks" :key="task.id" clickable v-ripple @click="openProject(task.url)">
            <q-item-section>{{ task.name }}</q-item-section>
          </q-item>
        </q-list>
      </q-btn-dropdown>
    </q-toolbar>
  </template>
  
  <script>
  export default {
    name: 'Navbar',
    data() {
      return {
        tasks: [
          { id: 1, name: 'Tugas1', url: 'https://project-cv-pbk-beta.vercel.app' },
          { id: 2, name: 'Tugas2', url: 'https://tugas2-risbul-223510089.vercel.app' },
          { id: 3, name: 'Tugas3', url: 'https://tugas3-riskibuulolo-223510089.vercel.app' },
          { id: 4, name: 'Tugas4', url: 'https://tugas4-riskibuulolo-223510089.vercel.app' },
          { id: 5, name: 'Tugas5', url: 'https://tugas5-riskibuulolo-223510089.vercel.app' },
          { id: 6, name: 'Tugas6', url: 'https://tugas6-riskibuulolo-223510089.vercel.app' },
          { id: 7, name: 'Tugas7', url: 'https://tugas7-riskibuulolo-223510089.vercel.app' },
        ],
      };
    },
    methods: {
      openProject(url) {
        window.open(url, '_blank');
      },
    },
  };
  </script>