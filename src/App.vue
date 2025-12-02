<script setup lang="ts">
import { ref, onMounted } from 'vue'
import TresScene from '@/components/TresScene.vue'

const calculator = ref<HTMLDivElement | null>(null)

const calculatorTop = ref<string | number>('unset')
const calculatorBottom = ref<string | number>('45px')
const calculatorTranslation = ref<string | number>('-50%, 100%')
const arrowRotateX = ref<string | number>(0)

const toggleCalculator = () => {
  calculatorBottom.value = calculatorBottom.value == '45px' ? 0 : '45px'
  calculatorTranslation.value = calculatorTranslation.value == '-50%' ? '-50%, 100%' : '-50%'
  arrowRotateX.value = arrowRotateX.value == 0 ? '180deg' : 0

  if (calculator.value?.clientHeight && calculator.value?.clientHeight + 30 > window.innerHeight) {
    calculatorTop.value = calculatorTop.value == '30px' ? 'unset' : '30px'
  }
}

const pi = Math.round(Math.PI * 100) / 100

const r = ref(2)
const h = ref(3)

const radius = ref(2)
const height = ref(3)

const l = ref(Math.round(Math.sqrt(r.value * r.value + h.value * h.value) * 100) / 100)

const calculate = () => {
  r.value = radius.value
  h.value = height.value

  toggleCalculator()
}

const getTwoNumbers = (n: number): number => {
  return (Math.round(n * 100) / 100)
}

onMounted(() => {
  calculator.value = document.querySelector('.cone')
})
</script>

<template>
  <main>
    <TresScene :r="r" :h="h" />

    <div class="cone">
      <img src="@/assets/images/arrow-up.png" alt="Arrow" @click="toggleCalculator">

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
  top: v-bind(calculatorTop);
  bottom: v-bind(calculatorBottom);
  left: 50%;
  transform: translate(v-bind(calculatorTranslation));
  transition: 0.5s;
  background-color: #002e92;
  color: #fff;
  display: grid;
  gap: 20px;
  padding: 40px;
  border-radius: 30px 30px 0 0;
  overflow: auto;
}

img {
  width: 20px;
  position: absolute;
  top: 15px;
  left: 50%;
  transform: translateX(-50%) rotateX(v-bind(arrowRotateX));
  transition: 0.5s;
  cursor: pointer;
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
