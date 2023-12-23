<script setup lang="ts">
import { ref, computed } from "vue";

type InitialData = {
  perspective: number;
  rotateX: number;
  rotateY: number;
  rotateZ: number;
};

const initialData = ref<InitialData>({
  perspective: 100,
  rotateX: 0,
  rotateY: 0,
  rotateZ: 0,
});

const computeBox = () => {
  return {
    transform: `perspective(${initialData.value.perspective}px) rotateX(${initialData.value.rotateX}deg) rotateY(${initialData.value.rotateY}deg) rotateZ(${initialData.value.rotateZ}deg)`,
  };
};

const box = computed(computeBox);

function reset(this: any) {
  initialData.value.perspective = 100;
  initialData.value.rotateX = 0;
  initialData.value.rotateY = 0;
  initialData.value.rotateZ = 0;
}

async function copy(this: any) {
  let text = `transform:${computeBox().transform}`;
  await navigator.clipboard.writeText(text);
  alert("CSS Copied to Clipboard!");
}
</script>

<template>
  <h2>CSS3 Perspective Playground</h2>
  <main>
    <section class="settings">
      <div class="settings-container">
        <label>perspective: {{ initialData.perspective }} px;</label>
        <input
          type="range"
          min="0"
          max="999"
          v-model="initialData.perspective"
        />

        <label>rotateX: {{ initialData.rotateX }} deg; </label>
        <input
          type="range"
          min="-180"
          max="180"
          v-model="initialData.rotateX"
        />

        <label>rotateY: {{ initialData.rotateY }} deg; </label>
        <input
          type="range"
          min="-180"
          max="180"
          v-model="initialData.rotateY"
        />

        <label>rotateZ: {{ initialData.rotateZ }} deg; </label>
        <input
          type="range"
          min="-180"
          max="180"
          v-model="initialData.rotateZ"
        />

        <button type="button" @click.prevent="reset">Reset</button>
        <button type="button" @click.prevent="copy">Copy</button>
      </div>
    </section>
    <section class="output">
      <div class="box-container">
        <div class="box" :style="box"></div>
      </div>
    </section>
  </main>
</template>
