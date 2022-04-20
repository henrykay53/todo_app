<template>
  <h1>TODO APP</h1>

  <form @submit.prevent="addNewTodo">

    <input  v-model="newTodo" type="text" placeholder="Enter Text" class="form-ctl">
    <button class="submitBtn">SUBMIT</button>

  </form>



  <ul>

    <li v-for="(todo, index) in todos" :key="todo.id" class="cursor">
      <h3 :class="{done: todo.done}" @click="toggleDone(todo)">{{todo.content}}</h3>
      <button class="remove-todo" @click="removeTodo(index)">Remove Todo</button>
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
      // todo.done = !todo.done;
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


<style scoped>
  h1 {
    text-align: center;
    margin-top: 40px;
  }

  form {
    display: flex;
    justify-content: center;
    margin-top: 40px;
  }

  input  {
    padding: 10px 60px;
    border-radius: 10px;
    border: 1px solid black;
  }

  /* input::placeholder {
    margin-right: 100px;
  } */

  .submitBtn {
    margin-left: 10px;
    background: green;
    border-radius: 10px;
    border: none;
  }

  .submitBtn:hover {
    padding: 0px 10px;
    /* transition: 1s ease-in-out; */
  }

  /* ul {
 
  } */

  li:nth-child(1) {
    margin-top: 20px;
  }

  li {
    display: flex;
    background: green;
    border-radius: 10px;
    align-content: center;
    justify-content: space-evenly;
    /* list-style: none; */
    font-size: 25px;
    padding: 10px 0;
    margin-top: 20px;
    margin-bottom: 10px;
    margin-left: 0;
  
  }

  .remove-todo {

    background: red;
    border-radius: 10px;
    padding: 10px 60px;
    border: none;
    margin-left: 

  }

  .cursor {
    cursor: pointer;
  }

  .done {
    text-decoration: line-through;
    color: red;

  }


  .span-flex {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 30px;
    margin-right: 10px;
  }

  .span-flex > button {
    border-radius: 10px;
    padding: 10px 60px;
    border: none;
    margin-left: 10px;

  }

  .remove {
    background: red;
  }

  .mark {
    background: green;
  }

</style>
