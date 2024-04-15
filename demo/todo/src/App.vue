<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>
<template>
  <div id="app">
    <h1>To-Do List</h1><br>
    <div class="input-container">
      <input type="text" v-model="newTodo" @keyup.enter="addTodo" placeholder="Add your to-do list">
      <button class="add-button" @click="addTodo">+</button>
    </div><br>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
      <div class="list-item">
        <input type="checkbox" v-model="todo.completed">
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <button class="delete-button" @click="removeTodo(index)">Delete</button>
        </div>
      </li><br>
    </ul>
    <button class="clear-button" @click="clearCompleted">Clear Completed</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: []
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, completed: false });
        this.newTodo = '';
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed);
    }
  }
};
</script>

<style scoped>
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f0f0f0;
  padding: 0;
  display: flex;
  margin-left: 300px;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app {
  max-width: 600px;
  margin: 20px auto;
  margin-left:40px;
  background-color: #fff;
  border-radius: 8px;
  padding: 30px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column; /* Ensure items stack vertically */
  align-items: center; /* Center items horizontally */
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
  margin-top: 0; /* Remove top margin */
}

.input-container {
  display: flex;
  align-items: center;
}

input[type="text"] {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  margin-right: 30px;
}

.add-button {
  background-color: #5cb85c;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 5px;
  cursor: pointer;
  margin-left:30px;
  margin-right:30px;
}

.add-button:hover {
  background-color: #4cae4c;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  background-color: #f9f9f9;
  padding: 15px;
  border-radius: 5px;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.delete-button {
  background-color: #d9534f;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-right:60px;
  margin-left:100px;
}

.delete-button:hover {
  background-color: #c9302c;
}

.clear-button {
  background-color: #f0ad4e;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-size: 16px;
  margin-top: 20px;
}

.clear-button:hover {
  background-color: #eea236;
}

.completed {
  text-decoration: line-through;
  text-color:black;
}

.list-item input[type="checkbox"] {
  margin-right: 30px; /* Adjust margin as needed */
  
}
.list-item span {
  color: black !important; /* Override text color */
}


</style>
