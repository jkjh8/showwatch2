<script setup>
import { useQuasar } from 'quasar'
import moment from 'moment'
import { clock } from 'src/composables/useClock'
const $q = useQuasar()
$q.dark.set(true)
moment.locale('KO')
</script>

<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-black">
      <q-toolbar>
        <q-icon name="timer" size="md" color="blue-grey-4" />
        <q-toolbar-title>
          {{ moment(clock).format('YYYY-HH-DD dddd') }}
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>
