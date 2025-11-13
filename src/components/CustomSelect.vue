<script setup lang="ts">
import { ref } from 'vue'

const props = defineProps<{
  options: Array<string | number>
  currentOptionIndex: number
  selectOption: (index: number) => void
  width: number
}>()

const width = ref<string>(`${props.width}px`)
const height = ref<string>(`calc(${100 * props.options.length}% - ${2 * props.options.length}px`)
</script>

<template>
  <div class="custom-select pointer">
    <aside class="current-option bold">
      {{ options[currentOptionIndex] == -1 ? 'All' : options[currentOptionIndex] }}
      <!-- <Icon name="mdi:chevron-up" size="20px" style="color: #000;" class="arrow" /> -->
      <img src="@/assets/images/arrow-up.png" alt="Arrow Up" class="arrow">
    </aside>

    <div class="options">
      <aside
        v-for="(option, index) in options"
        :key="index"
        @click="selectOption(index)"
        :class="index == currentOptionIndex ? 'bold' : ''"
      >
        {{ option == -1 ? 'All' : option }}
      </aside>
    </div>
  </div>
</template>

<style scoped>
.custom-select {
  position: relative;
  width: v-bind(width);
  cursor: pointer;
}

.current-option,
.options aside {
  width: v-bind(width);
  background-color: var(--main-color);
  color: #fff;
  padding: 15px;
  border: solid #fff;
  border-width: 0 2px 2px 2px;
}

.current-option {
  border-top-width: 2px;
}

.current-option .arrow {
  width: 15px;
  position: absolute;
  right: 15px;
}

.custom-select:hover .current-option .arrow {
  transform: rotate(-180deg);
}

.options {
  position: absolute;
  height: 0%;
  overflow: hidden;
  transition: 0.4s;
  z-index: 10;
}

.custom-select:hover .options {
  height: v-bind(height);
}

.options aside:hover {
  background-color: #fff;
  color: var(--main-color);
}
</style>
