<script setup>
  // import { defineProps, defineEmits } from 'vue'
  import {ref} from "vue";

  const props = defineProps(['text'])
  const emit = defineEmits(['change'])
  const arr = ref([
    'China',
    'Japan',
    'Usa',
    'France',
    'England',
    'Brazil',
    'Korea',
    'Mexico',
    'Vietnam',
    'Pakistan'
  ]);

  function send() {
    emit('change',arr.value[Math.floor(Math.random() * 10)]);
  }
</script>

<template>
  <div class="button" @click="send"> {{props.text}} </div>
</template>

<style scoped>
.button{
  margin: 100px 0 0 200px;
  width: 100px;
  height: 50px;
  line-height: 50px;
  text-align: center;
  background-color: antiquewhite;
  border-radius: 10px;
  cursor: pointer;
  user-select: none;
}
</style>