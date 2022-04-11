<script setup>
import { ref, computed } from 'vue'
import moment from 'moment'
import {
  clock,
  toggleStart,
  showTime,
  status,
  second,
  fnStop,
  start,
  remaind,
  remaindTime
} from 'src/composables/useClock'

const visi = ref(false)

function fnStart() {
  toggleStart()
  visi.value = true
}
function fnReset() {
  fnStop()
  visi.value = false
}
</script>

<template>
  <q-page class="flex flex-center">
    <div>
      <div class="name-tag">현재시간</div>
      <div style="margin-top: -8vmin">
        <span :class="visi ? 'clock-duration' : 'clock-nomal'">
          {{ moment(clock).format('hh:mm:ss') }}
        </span>
        <span style="font-size: 10vmin">
          {{ moment(clock).format('a') }}
        </span>
      </div>
      <div v-if="visi" style="margin-top: -7vmin">
        <div class="row no-wrap justify-between">
          <div>
            <div class="name-tag">시작시간</div>
            <div class="text-yellow-8" style="margin-top: -2vmin">
              <span style="font-size: 10vmin">
                {{ moment(start).format('hh:mm:ss') }}
              </span>
              <span style="font-size: 2vmin">
                {{ moment(start).format('a') }}
              </span>
            </div>
          </div>
          <div>
            <div class="name-tag">지속시간</div>
            <div
              class="text-yellow-8"
              style="font-size: 11vmin; margin-top: -2vmin"
            >
              {{ remaindTime }}
            </div>
          </div>
        </div>
        <div class="name-tag">경과시간</div>
        <div class="clock-nomal" style="margin-top: -10vmin">
          {{ showTime }}
        </div>
      </div>
    </div>

    <q-page-sticky position="bottom-right" :offset="[18, 18]">
      <q-btn
        round
        :color="status ? 'yellow' : 'primary'"
        :icon="status ? 'pause' : 'play_arrow'"
        @click="fnStart"
      />
      <q-btn
        v-if="second"
        class="q-ml-sm"
        round
        color="red-10"
        icon="stop"
        @click="fnReset"
      />
    </q-page-sticky>
    <q-page-sticky position="bottom-right" :offset="[18, 68]">
      <q-btn round icon="visibility" color="blue-grey" @click="visi = !visi" />
    </q-page-sticky>
  </q-page>
</template>

<style>
.clock-nomal {
  font-size: 32vmin;
}
.clock-duration {
  font-size: 27vmin;
}
.name-tag {
  font-size: 3vmin;
}
</style>
