<script setup lang="ts">
import { ref } from 'vue'
import TresScene from '@/components/TresScene.vue'

const cylinderRadius = ref(2)
const cylinderHeight = ref(4)
const cylinderColor = ref('#182d8e')
</script>

<template>
  <main>
    <TresScene :cylinderRadius="cylinderRadius" :cylinderHeight="cylinderHeight" :cylinderColor="cylinderColor" />

    <div class="cylinder-parameters">
      <h2>Cylinder Parameters</h2>

      <input type="number" placeholder="Cylinder Radius" v-model="cylinderRadius">
      <input type="number" placeholder="Cylinder Height" v-model="cylinderHeight">
      <input type="color" placeholder="Cylinder Color" v-model="cylinderColor">
    </div>
  </main>
</template>

<style scoped>
.cylinder-parameters {
    position: fixed;
    top: 50%;
    right: 100px;
    transform: translateY(-50%);
    background-color: #002e92;
    color: #fff;
    display: grid;
    gap: 20px;
    padding: 40px;
    border-radius: 20px;
}

.cylinder-parameters h2 {
    padding: 0 40px;
}
</style>
