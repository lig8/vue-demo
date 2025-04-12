<script setup>
  import myButton from "./components/button.vue";
  import {ref} from "vue";

  const msg = ref('start');
  function change(str){
    msg.value = str;
  }
</script>

<template>
  <myButton :text = "msg" @change="change"> </myButton>
  <myButton text= '我好'> </myButton>
  <myButton  text= '大家好'> </myButton>
</template>

<style scoped></style>