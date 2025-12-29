<template>
  <q-layout view="hHh 1pR fFf">

    <!--Header-->
    <q-header elevated class="bg-primary text-white">
      <q-toolbar>
        <q-btn
         flat 
         dense
         round
         icon="menu"
         @click="leftDrawerOpen = !leftDrawerOpen"/>
      <q-toolbar-title>Student App</q-toolbar-title>
      </q-toolbar>
    </q-header>

    <!--Drawer-->
    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item clickable to="/">
          <q-item-section>Home</q-item-section>
        </q-item>
        <q-item clickable :to="{ path: '/students'}">
          <q-item-section>Students</q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <!--Page Container-->
    <q-page-container>
      <router-view />
    </q-page-container>

    <!--Footer-->
    <q-footer class="bg-grey-2 text-center">
      <div class="q-pa-sm">2025 Student App</div>
    </q-footer>

  </q-layout>
  </template>

  <script>
    export default  {
      name: 'MainLayout',

      data () {
        return {
          leftDrawerOpen: false
        }
      }
    }
  </script>