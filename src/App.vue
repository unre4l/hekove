<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { ref } from 'vue';

const pwm = ref(0);

async function post (key: string, value: string|number) {
  const data = new FormData();
  data.set(key, `${value}`);
  const response = await fetch('/set', { method: 'post', body: data});
  const respData = await response.json() as { value: string|number };
  console.log(respData.value);
}

async function setPwm(value: number) {
  await post('dutyCycle', value);
  pwm.value = value;
}
</script>

<template>
  <nav>

  </nav>

  <div>
    {{  pwm  }}
    <input :value="pwm" @change="(e: Event) => setPwm(e.target.value)" type="range" min="0" max="255">
  </div>

  <RouterView />
</template>

