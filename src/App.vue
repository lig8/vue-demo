<script setup>
  import {ref} from "vue";
  import axios from "axios"

  const str = ref('');
  const list = ref([]);

 async function getList(){
    const res = await axios({
      url:"https://acx740jken.gzg.sealos.run/get_list",
      method: "GET"
    });
    list.value = res.data.list;
   // console.log(list);
 }

  async function addTodo(){
    const res = await axios({
      url:"https://acx740jken.gzg.sealos.run/add_todo",
      method: "POST",
      data:{
        value: str.value,
        isCompleted: false
      }
    });
    str.value = "";
    getList();
  }

  async function updateTodo(id){
    const res = await axios({
      url:"https://acx740jken.gzg.sealos.run/update_todo",
      method: "PUT",
      data:{id}
    });
    getList();
  }

  async function deleteTodo(id){
    const res = await axios({
      url:"https://acx740jken.gzg.sealos.run/delete_todo",
      method: "delete",
      data:{ id }
    });
    getList();
  }

  getList();

</script>

<template>
  <div class="todo-App">

<!--  title  -->
    <div class = "title"> XXX的todo-App </div>

<!--  add todo  -->
    <div class="todo-form">
      <input v-model="str" class="todo-input" type="text" placeholder="add a todo">
      <div @click="addTodo" class="todo-button">add todo</div>
    </div>

<!--  items  -->
    <div v-for='(item) in list' :class="[item.isCompleted ? 'item completed' : 'item']">
      <div>
        <input v-model="item.isCompleted" @click="updateTodo(item._id)" type="checkbox" />
        <span class="name"> {{ item.value}} </span>
      </div>
      <div @click="deleteTodo(item._id)" class="del"> del </div>
    </div>

  </div>
</template>

<style>

.name{
  margin-left: 10px;
}
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
  box-shadow:  rgba(149, 157, 165, 0.2) 0 8px 20px;
}
.todo-form{
  display: flex;
  margin-top: 20px;
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