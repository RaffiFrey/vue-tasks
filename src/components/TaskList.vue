﻿<script setup lang="ts">
import type {Task} from "../types.ts";

const props = defineProps<{
  tasks: Task[]
}>();

const emits = defineEmits<{
  toggleDone: [id: string],
  removeTask: [id: string]
}>()
</script>

<template>
  <TransitionGroup name="list" tag="div" class="task-list">
    <article v-for="task in props.tasks" class="task" :key="task.id">
      <label>
        <input @input="emits('toggleDone', task.id)" :checked="task.done" type="checkbox">
        <span :class="{ done: task.done}">{{ task.title }}</span>
      </label>
      <button @click="emits('removeTask', task.id)" class="outline">Remove</button>
    </article>
  </TransitionGroup>
</template>

<style scoped>

.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-list {
  margin-top: 1rem;
}

.done {
  text-decoration: line-through;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>