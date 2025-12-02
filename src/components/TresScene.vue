<script setup lang="ts">
import { TextureLoader } from 'three'
import { TresCanvas, useLoader } from '@tresjs/core'
import { OrbitControls } from '@tresjs/cientos'

defineProps<{
  r: number
  h: number
}>()

const { state: texture } = useLoader(TextureLoader, './texture.jpg')
</script>

<template>
   <TresCanvas clear-color="#29adff" window-size>
    <TresPerspectiveCamera :position="[1, 5, 10]" :look-at="[0, 0, 0]" />

    <TresAmbientLight :intensity="0.5" />
    <TresDirectionalLight :position="[10, 10, 10]" />

    <OrbitControls :minDistance="0.5" :maxDistance="100" :zoom-speed="0.5" />

    <TresMesh :position="[0, - h / 4, 0]">
      <TresCylinderGeometry :args="[r * 0.9, r * 0.9, h / 2]" />
      <TresMeshStandardMaterial v-if="texture" :map="texture" />
    </TresMesh>

    <TresMesh :position="[0, h / 2, 0]">
      <TresConeGeometry :args="[r, h]" />
      <TresMeshStandardMaterial v-if="texture" :map="texture" />
    </TresMesh>
  </TresCanvas>
</template>

<style scoped>

</style>
