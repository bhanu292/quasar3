<template>
  <q-page class="q-pa-md">
    <h5>Dashboard</h5>
    <q-row gutter="16">
      <q-col cols="12" md="6">
        <q-card>
          <q-card-section>
            <div class="text-h6">Students</div>
            <p>Total students registered</p>
          </q-card-section>
        </q-card>
      </q-col>

      <q-col cols="12" md="6">
        <q-card>
          <q-card-section>
            <div class="text-h6">Reports</div>
            <p>Monthly reports overview</p>
          </q-card-section>
        </q-card>
      </q-col>

    </q-row>

  </q-page>
  </template>

  <script>
    export default {
      name: 'IndexPage'
    }
  </script>