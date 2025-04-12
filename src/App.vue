<script setup>
import {ref, watch } from "vue";

function add(newVal, oldVal) {
  console.log('newVal: '+ newVal, 'oldVal: '+ oldVal);
}

function del(index){
  list.value.splice(index, 1);
}

const str = ref('');

const list = ref([
  {
    isCompleted: true,
    text: '吃饭'
  },
  {
    isCompleted: false,
    text: '睡觉'
  },
  {
    isCompleted: false,
    text: '打豆豆'
  }
]);

watch(str,add);
</script>

<template>
  <div class="todo-App">

    <!--  title  -->
    <div class = "title"> XXX的todo-App </div>

    <!--  add todo  -->
    <div class="todo-form">
      <input v-model="str" class="todo-input" type="text" placeholder="add a todo">
      <div @click="add" class="todo-button">add todo</div>
    </div>

    <!--  items  -->
    <div v-for='(item,index) in list' :class="[item.isCompleted ? 'item completed' : 'item']">
      <div>
        <input v-model="item.isCompleted" type="checkbox" />
        <span class="name"> {{ item.text}} </span>
      </div>
      <div @click="del(index)" class="del"> del </div>
    </div>

  </div>
</template>

<style>
.completed {
  text-decoration: line-through;
  opacity: 0.4;
}
.del{
  color: red;
  cursor: pointer;
}

.item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  box-sizing: border-box;
  width: 80%;
  height: 50px;
  margin: 8px auto;
  padding: 16px;
  border-radius: 20px;
  box-shadow:  rgba(149, 157, 165, 0.2) 0px 8px 20px;
}
.todo-form{
  display: flex;
  marging-top: 20px;
  margin-left: 30px;
}

.todo-input{
  padding-left: 15px;
  margin-bottom: 20px;
  width: 60%;
  height: 50px;
  border: 1px solid #dfe1e5;
  outline: none;
  border-radius: 20px 0 0 20px;
}

.todo-button{
  width: 100px;
  height: 52px;
  border-radius: 0 20px 20px 0;
  text-align: center;
  line-height: 52px;
  color: #fff;
  background: linear-gradient(to right, rgb(113,65,168), rgba(44,114,251,1));
  cursor: pointer;
  user-select: none;
}

body {
  margin: 10px;
  min-height: 100vh;
  background: linear-gradient(to right, rgb(113,65,168), rgba(44,114,251,1));
}
.todo-App{
  padding-top: 30px;
  box-sizing: border-box;
  width: 98%;
  margin-top: 40px;
  margin-left: 1%;
  height: 500px;
  background: white;
  border-radius: 5%;
}
.title{
  font-size: 30px;
  font-weight: 700;
  text-align: center;
}
</style>