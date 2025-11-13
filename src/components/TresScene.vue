<script setup lang="ts">
import { TresCanvas } from '@tresjs/core'
import { OrbitControls } from '@tresjs/cientos'
import { meshes } from '@/types/models'

defineProps<{
  meshType: meshes
  radius: number
  height: number
  color: string
}>()
</script>

<template>
   <TresCanvas clear-color="#617aea" window-size>
    <TresPerspectiveCamera :position="[0, 0, 40]" :look-at="[0, 0, 0]" />

    <TresAmbientLight :intensity="0.5" />
    <TresDirectionalLight :position="[10, 10, 10]" />

    <OrbitControls :minDistance="5" :maxDistance="20" :zoom-speed="0.5" />

    <TresMesh>
      <TresSphereGeometry :args="[radius]" v-if="meshType == meshes.Sphere" />
      <TresCylinderGeometry v-else-if="meshType == meshes.Cylinder" :args="[radius, radius, height, 100]" />
      <TresConeGeometry v-else />

      <TresMeshStandardMaterial :color="color" />
    </TresMesh>
  </TresCanvas>
</template>

<style scoped>

</style>
