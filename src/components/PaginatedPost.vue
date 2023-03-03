<script setup>
import { computed } from 'vue';
  defineProps(['inicio', 'fin','postsLength'])
  

</script>

<template>

<div class="btn-group" role="group" aria-label="Basic example">
  <button 
    type="button" 
    class="btn btn-primary" 
    @click="$emit('prev')"
    :disabled="inicio === 0"
  >
  Previous </button>
  <button type="button"
    class="btn
    btn-primary"
     @click="$emit('next')"
     :disabled="fin === postsLength"
     >
  Next</button>
</div>

</template>