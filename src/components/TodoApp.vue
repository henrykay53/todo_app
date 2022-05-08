<template>
  <h1>TODO APP</h1>

  <form @submit.prevent="addNewTodo">

    <input  v-model="newTodo" type="text" placeholder="Enter Task" class="input">
    <button class="submitBtn">SUBMIT</button>

  </form>

  <ul>

    <li v-for="(todo, index) in todos" :key="todo.id" class="cursor">
      <h3  class="tasks" :class="{done: todo.done}" @click="toggleDone(todo)">{{todo.content}}</h3>

      <div class="alg-self">
        <button class="remove-todo" @click="removeTodo(index)">REMOVE TODO</button>
      </div>

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
    padding: 10px 50px;
    border-radius: 10px;
    border: 1px solid rgb(81, 216, 81);
  }

  input:focus {
    outline: none;
  }

  .submitBtn {
    margin-left: 10px;
    background: rgb(81, 216, 81);
    border-radius: 10px;
    border: none;
    color: black !important;
  }

  .submitBtn:hover {
    padding: 0px 10px;
  }

  ul {
    padding-inline-start: 0;
    width: 100%;
    margin-left: auto;
    margin-right: auto;
  }

  li {
    display: flex;
    align-content: center;
    justify-content: space-between;
    background: grey;
    border-radius: 10px;
    font-size: 25px;
    color: black !important;
    margin: 30px 60px;
    padding: 15px;
  }

  .tasks {
    margin-left: 50px;
  }

  .remove-todo {
    align-self: flex-end;
    background: rgb(235, 51, 51);
    border-radius: 10px;
    padding: 10px 60px;
    border: none;
    color: black !important;
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
    color: black !important;
  }

  .mark {
    background: rgb(81, 216, 81);
    color: black !important;
  }

  /* Media query for mobile */

  @media (max-width: 500px) {

  
    ul {
      width: 100%;
    }

    li {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-left: 10px;
      margin-right: 10px;
      font-size: 15px;
      padding: 10px;
    
    }

    .tasks {
      margin-left: 0;
    }


    .remove-todo {
      padding: 10px; 
      color: black !important;
    }

    .remove, .mark {
      color: black !important;
    }

  }

  /* Media query for tablet */

  @media(min-width: 501px) and (max-width: 1024px) {

    ul {
      width: 100%;
    }
  }  


</style>