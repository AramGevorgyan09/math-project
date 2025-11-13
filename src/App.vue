<script setup lang="ts">
import { ref, reactive } from 'vue'
import TresScene from '@/components/TresScene.vue'
import CustomSelect from './components/CustomSelect.vue'
import { meshes } from './types/models'

const allMeshes = reactive<meshes[]>([meshes.Sphere, meshes.Cylinder, meshes.Cone])

const mesh = ref<meshes>(meshes.Sphere)
const radius = ref(2)
const height = ref(4)
const color = ref('#182d8e')

const selectMesh = (index: number) => {
  if (allMeshes[index]) {
    mesh.value = allMeshes[index]
  }
}
</script>

<template>
  <main>
    <TresScene :mesh-type="mesh" :radius="radius" :height="height" :color="color" />

    <div class="cylinder-parameters">
      <h2>Cylinder Parameters</h2>

      <CustomSelect :options="allMeshes" :current-option-index="0" :select-option="selectMesh" :width="200" />
      <input type="number" placeholder="Radius" v-model="radius" v-if="radius">
      <input type="number" placeholder="Height" v-model="height">
      <input type="color" placeholder="Color" v-model="color">
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
