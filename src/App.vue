<script setup lang="ts">
import { ref } from 'vue'
import TresScene from '@/components/TresScene.vue'

const pi = Math.round(Math.PI * 100) / 100

const r = ref(2)
const h = ref(3)

const radius = ref(2)
const height = ref(3)

const l = ref(Math.round(Math.sqrt(r.value * r.value + h.value * h.value) * 100) / 100)

const calculate = () => {
  r.value = radius.value
  h.value = height.value
}

const getTwoNumbers = (n: number): number => {
  return (Math.round(n * 100) / 100)
}
</script>

<template>
  <main>
    <TresScene :r="r" :h="h" />

    <div class="cone">
      <h1>Կոն</h1>

      <input type="number" placeholder="Շառավիղ" v-model="radius">
      <input type="number" placeholder="Բարձրություն" v-model="height">
      <button type="button" @click="calculate">Հաշվել</button>

      <p>
        <span class="name">Կողմնային մակերևույթի մակերես՝<br></span>
        <span class="formula">S<sub>կ</sub> = &#x3C0;rl &#8776; {{ pi }} &#215; {{ r }} &#215; {{ l }} = {{ getTwoNumbers(pi * r * l) }}<br></span>
        <span class="name">Հիմքի մակերես՝<br></span>
        <span class="formula">S<sub>հ</sub> = &#x3C0;r<sup>2</sup> &#8776; {{ pi }} &#215; {{ r }} &#215; {{ r }} = {{ getTwoNumbers(pi * r * r) }}<br></span>
        <span class="name">Լրիվ մակերևութային մակերես՝<br></span>
        <span class="formula">S<sub>լ</sub> = S<sub>կ</sub> + S<sub>հ</sub> = &#x3C0;rl + &#x3C0;r<sup>2</sup> &#8776; {{ pi }} &#215; {{ r }} &#215; {{ l }} + {{ pi }} &#215; {{ r }} &#215; {{ r }} = {{ getTwoNumbers(pi * r * l + pi * r * r) }}</span>
      </p>
    </div>
  </main>
</template>

<style scoped>
.cone {
  position: fixed;
  top: 50%;
  right: 40px;
  transform: translateY(-50%);
  background-color: #002e92;
  color: #fff;
  display: grid;
  gap: 20px;
  padding: 40px;
  border-radius: 20px;
}

h1 {
  text-align: center;
}

button {
  justify-self: center;
}

p {
  max-width: 400px;
  display: grid;
  gap: 15px;
}

.name {
  font-size: 16px;
  color: #ddd;
}

.formula {
  font-size: 20px;
  border: 2px solid #fff;
  padding: 10px;
  line-height: 150%;
}
</style>
