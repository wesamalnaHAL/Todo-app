<script setup>
import { ref } from "vue";

const newTodo = ref("");
const todos = ref([]);
const editingTodoIndex = ref(-1);

const addTodo = () => {
  if(newTodo.value.trim()!== "") {
    todos.value.push({text : newTodo.value, editing: false});
    newTodo.value= ""
  }
};

const removeTodo = (index) => {
  todos.value.splice(index,1)
}

const startEditing = (index) => {
  editingTodoIndex.value = index;
};

const saveChanges = (index) => {
  todos.value[index].editing = false;
  editingTodoIndex.value = -1;
};
const removeAll = () => {
  todos.value = []
}
</script>

<template>
  <div class="todo-app">
    <h1>Todo App</h1>
    <div class="todo-input">
      <input v-model="newTodo" placeholder="Enter a new todo" />
      <button @click="addTodo">Add Todo</button>
    </div>
    <ul class="todo-list">
      <li v-for="(todo, index) in todos" :key="index">
        <span v-if="index !== editingTodoIndex">{{ todo.text }}</span>
        <input v-else v-model="todo.text" @keyup.enter="saveChanges(index)" />
        <button class="rem" @click="removeTodo(index)">Remove</button>
        <button v-if="index !== editingTodoIndex" @click="startEditing(index)">Edit</button>
        <button v-else @click="saveChanges(index)">Save</button>
      </li>
      <button v-if="todos != ''" @click="removeAll" class="clear-all">Clear all</button>
    </ul>
  </div>
</template>

<!-- ...CSS styles remain the same... -->

<style scoped>
.todo-app {
  font-family: Arial, sans-serif;
  max-width: 400px;
  margin: 0 auto;
  background-color: #f8f8f8;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  margin-top: 20px;
  margin-bottom: 30px;
  color: #555;
  font-size: 28px;
  text-transform: uppercase;
}

.todo-input {
  display: flex;
  margin-bottom: 20px;
}
.rem {
  margin-right: 5px;
}

.todo-input input {
  flex: 1;
  padding: 12px;
  font-size: 16px;
  border: none;
  border-bottom: 2px solid #999;
  outline: none;
  transition: border-color 0.3s ease;
}

.todo-input input:focus {
  border-color: #4caf50;
}

.todo-input button {
  padding: 12px 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.todo-input button:hover {
  background-color: #45a049;
}

.todo-list {
  list-style-type: none;
  padding: 0;
}

.todo-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  border-bottom: 1px solid #eee;
  transition: background-color 0.3s ease;
}

.todo-list li:last-child {
  border-bottom: none;
}

.todo-list li:hover {
  background-color: #f2f2f2;
}

.todo-list li button {
  background-color: #f44336;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  font-size: 14px;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.todo-list li button.edit-button {
  background-color: #2196f3;
  margin-right: 10px;
}

.todo-list li button:hover {
  background-color: #e53935;
}

.todo-list li span {
  flex: 1;
  margin-right: 10px;
  font-size: 16px;
  word-break: break-word;
}

.todo-list li input {
  flex: 1;
  padding: 5px;
  font-size: 16px;
  border: none;
  border-bottom: 2px solid #999;
  outline: none;
  transition: border-color 0.3s ease;
}

.todo-list li input:focus {
  border-color: #4caf50;
}
.todo-list button.clear-all {
  margin-top: 10px;
  padding: 8px 16px;
  background-color: #ff5722;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.todo-list button.clear-all:hover {
  background-color: #e64a19;
}
</style>
