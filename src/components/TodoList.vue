<template>
  <div class="wrapper">
    <div class="todo-list">
      <div class="list-controller">
        <h2>Work list</h2>
        <input type="text" v-model="newTodo" placeholder="Add new job" />
        <button @click="addTodo">Add</button>
      </div>
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <div class="item">
            <input
              type="checkbox"
              v-model="todo.done"
              :class="{ 'todo-item': true, done: todo.done }"
            />
            <span :class="{ 'todo-strikethrough': todo.done }">{{ todo.text }}</span>
          </div>
          <button @click="removeTodo(index)">Delete</button>
        </li>
      </ul>
    </div>
    <button @click="removeAllTodos">Delete all</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: "",
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({ text: this.newTodo, done: false });
        this.newTodo = "";
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    removeAllTodos() {
      this.todos = this.todos.filter(todo => !todo.done);
    },
  },
};
</script>

<style scoped>
.wrapper {
  width: 500px;
  margin: 0 auto;
}
.todo-list {
  font-family: sans-serif;
}

.list-controller {
  margin-bottom: 20px;
}

.item {
  width: 300px;
  flex: 0 0 auto;
  display: flex;
  justify-content: flex-start;
}

.todo-list ul {
  width: 400px;
  margin: 0 auto;
  list-style: none;
  padding: 0;
}

.todo-list li {
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.todo-list input[type="checkbox"] {
  margin-right: 10px;
}

.todo-list button {
  cursor: pointer;
  border: none;
  padding: 5px 10px;
  margin-left: 10px;
  background-color: #eee;
  border-radius: 5px;
  width: 100px;
  min-height: 50px;
  border: 1px solid;
}

input[type="text"] {
  padding: 10px;
  width: 300px;
  height: 50px;
}

.todo-strikethrough {
  text-decoration: line-through;
}

.hidden {
  display: none;
}
</style>
