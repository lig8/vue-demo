<script setup>
  import myButton from "./components/button.vue";

  function add(str){
    console.log(str)
  }
</script>

<template>
  <myButton text = "你好" @msg="add"> </myButton>
  <myButton text= '我好'> </myButton>
  <myButton  text= '大家好'> </myButton>
</template>

<style scoped></style>