<script setup>
import DecimalInput from './components/DecimalInput.vue';
import Header from "./components/Header.vue";
import Card from './components/Сard.vue'
</script>

<template>
  <Header />
  <div class="container mx-auto p-4 flex justify-center items-center">
    <Card
        title="Decimal Input Example"
        class="max-w-2xl"
    >
      <DecimalInput />
    </Card>

  </div>
</template>
