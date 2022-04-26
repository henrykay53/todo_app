<template>
  <h1>TODO APP</h1>

  <form @submit.prevent="addNewTodo">

    <input  v-model="newTodo" type="text" placeholder="Enter Task" class="input">
    <button class="submitBtn">SUBMIT</button>

  </form>

  <ul>

    <li v-for="(todo, index) in todos" :key="todo.id" class="cursor">
      <h3 :class="{done: todo.done}" @click="toggleDone(todo)">{{todo.content}}</h3>
      <button class="remove-todo" @click="removeTodo(index)">REMOVE TODO</button>
    </li>
  

  </ul>

  <span class="span-flex">
    <button class="remove" @click="RemoveAll">REMOVE ALL</button>
    <button  class="mark" @click="markAll">MARK ALL</button>
  </span>
  
</template>



<script>

import { ref } from 'vue';

export default {
  name: 'Todo',

  setup() {

    const newTodo = ref('');
    const todos = ref([]);
    
    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });

      newTodo.value = ''; 
    }

    function toggleDone(todo) {

      todo.done = !todo.done;

    }
 
    function removeTodo(index) {
      todos.value.splice(index, 1);

    }

    function markAll() {
      todos.value.forEach((todo) => todo.done = true)
    }

    
    function RemoveAll() {
      todos.value = [];
    }

    return {
      newTodo,
      todos,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAll,
      RemoveAll, 
    };
 
  }
  
}
</script>


<style>



  h1 {
    text-align: center;
    margin-top: 40px;
  }

  form {
    display: flex;
    justify-content: center;
    margin-top: 40px;
  }

  input[type="text"] {
    padding: 10px 60px;
    border-radius: 10px;
    border: 1px solid rgb(81, 216, 81);
    transition: all 0.6s ease-in-out;
  }

  input[type="text"]:focus {
    border: 1px solid gold;
  }

  .submitBtn {
    margin-left: 10px;
    background: rgb(81, 216, 81);
    border-radius: 10px;
    border: none;
  }

  .submitBtn:hover {
    padding: 0px 10px;
  }

  ul {
    padding-inline-start: 0;
    width: 50%;
    margin-left: auto;
    margin-right: auto;
  }

  li {
    display: flex;
    align-content: center;
    justify-content: space-evenly;
    background: grey;
    border-radius: 10px;
    font-size: 25px;
    margin: 30px 60px;
    padding: 15px 0;
  }

  .remove-todo {
    background: rgb(235, 51, 51);
    border-radius: 10px;
    padding: 10px 60px;
    border: none;
  }

  .cursor {
    cursor: pointer;
  }

  .done {
    text-decoration: line-through;
    color: black;
  }


  .span-flex {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 30px;
    margin-right: 10px;
    margin-bottom: 40px;
  }

  .span-flex > button {
    border-radius: 10px;
    padding: 10px 60px;
    border: none;
    margin-left: 10px;
  }

  .remove {
    background: rgb(235, 51, 51);
    border: none;
  }

  .mark {
    background: rgb(81, 216, 81);
  }

</style>
