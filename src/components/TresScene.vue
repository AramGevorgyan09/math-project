<script setup lang="ts">
import { TresCanvas } from '@tresjs/core'
import { OrbitControls } from '@tresjs/cientos'

defineProps<{
  cylinderRadius: number
  cylinderHeight: number
  cylinderColor: string
}>()
</script>

<template>
   <TresCanvas clear-color="#82dbc5" window-size>
    <TresPerspectiveCamera :position="[0, 0, 40]" :look-at="[0, 0, 0]" />

    <TresAmbientLight :intensity="0.5" />
    <TresDirectionalLight :position="[20, 20, 20]" />

    <OrbitControls :minDistance="5" :maxDistance="20" :enable-pan="false" :zoom-speed="0.4" />

    <TresMesh>
      <TresSphereGeometry />
      <TresMeshStandardMaterial color="#ff6b35" />
    </TresMesh>

    <!-- <TresMesh>
      <TresCylinderGeometry :args="[cylinderRadius, cylinderRadius, cylinderHeight, 100]" />
      <TresMeshBasicMaterial :color="cylinderColor" />
    </TresMesh> -->
  </TresCanvas>
</template>

<style scoped>

</style>
