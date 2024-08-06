<template>
  <div class="card border border-gray-300 bg-white p-4 rounded-lg shadow-sm w-full pb-12">
    <div v-if="title" class="card-header mb-6">
      <h3 class="text-lg font-semibold">{{ title }}</h3>
    </div>
    <div class="card-body">
      <slot></slot>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { defineProps } from 'vue';

interface CardProps {
  title?: string;
}

const props = defineProps<CardProps>();
</script>