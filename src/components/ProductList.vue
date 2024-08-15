<script setup>
import { defineProps, defineEmits } from 'vue'

defineProps(['data'])
const emit = defineEmits(['addCart'])
</script>

<template>
  <div class="col-md-4">
    <div class="list-group">
      <a
        href="#"
        class="list-group-item list-group-item-action"
        v-for="product in data"
        :key="product.id"
        @click="emit('addCart', product)"
      >
        <div class="d-flex w-100 justify-content-between">
          <h5 class="mb-1">{{ product.name }}</h5>
          <small>${{ product.price }}</small>
        </div>
        <p class="mb-1">{{ product.description }}</p>
      </a>
    </div>
  </div>
</template>
