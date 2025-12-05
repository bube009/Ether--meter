<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title>Ether Meter</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <h2>Niveau détecté : {{ value }}</h2>

      <ion-button expand="block" @click="start">Démarrer</ion-button>
      <ion-button expand="block" color="danger" @click="stop">Arrêter</ion-button>

      <canvas ref="canvas" style="margin-top:20px; width:100%; height:200px;"></canvas>
    </ion-content>
  </ion-page>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const value = ref(0)
const running = ref(false)
let ctx = null
const canvas = ref(null)

function start() {
  running.value = true
  loop()
}

function stop() {
  running.value = false
}

function loop() {
  if (!running.value) return
  value.value = Math.floor(Math.random() * 100)
  draw(value.value)
  requestAnimationFrame(loop)
}

function draw(v) {
  ctx.clearRect(0, 0, 300, 200)
  ctx.fillStyle = "#00ffff"
  ctx.fillRect(0, 200 - v * 2, 300, 200)
}

onMounted(() => {
  const c = canvas.value
  c.width = 300
  c.height = 200
  ctx = c.getContext("2d")
})
</script>o
