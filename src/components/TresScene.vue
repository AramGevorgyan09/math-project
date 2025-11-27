<script setup lang="ts">
import { TresCanvas } from '@tresjs/core'
import { OrbitControls } from '@tresjs/cientos'

defineProps<{
  r: number
  h: number
}>()
</script>

<template>
   <TresCanvas clear-color="#29adff" window-size>
    <TresPerspectiveCamera :position="[1, 5, 10]" :look-at="[0, 0, 0]" />

    <TresAmbientLight :intensity="0.5" />
    <TresDirectionalLight :position="[10, 10, 10]" />

    <OrbitControls :minDistance="5" :maxDistance="20" :zoom-speed="0.5" />

    <TresMesh>
      <TresConeGeometry :args="[r, h]" />
      <TresMeshStandardMaterial color="#6b79b8" />
    </TresMesh>
  </TresCanvas>
</template>

<style scoped>

</style>
