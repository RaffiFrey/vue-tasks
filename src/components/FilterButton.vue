﻿<script setup lang="ts">
import type {TaskFilter} from "../types.ts";

const props = defineProps<{
  filter: TaskFilter;
  currentFilter: TaskFilter;
}>();

const emits = defineEmits<{
  setFilter: [filter: TaskFilter]
}>();
</script>

<template>
  <button
      class="secondary"
      @click="emits('setFilter', props.filter)"
      :class="{ contrast: props.filter === props.currentFilter}"
  >
    {{props.filter}}
  </button>
</template>

<style scoped>
button {
  text-transform: capitalize;
}
</style>