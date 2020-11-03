<template>
  <div id="app">
    <div class="wrapper">
      <div class="container">
        <TodoInput @addTodo="addTodo" />
        <TodosList :todos="todos" @remove-todo="removeTodo" />
      </div>
    </div>
  </div>
</template>

<script>
import TodosList from "@/components/TodosList";
import TodoInput from "@/components/TodoInput";

export default {
  name: "App",
  data: () => ({
    todos: [],
    todoId: 1,
  }),
  methods: {
    addTodo(todo) {
      todo.id = this.todoId;
      this.todos.push(todo);
      this.todoId++;
    },
    removeTodo(id) {
      this.todos = this.todos.filter((t) => t.id !== id);
    },
  },
  components: {
    TodosList,
    TodoInput,
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
}

.lol {
  width: 100%;
  height: 100px;
  background-color: #fff;
}
.wrapper {
  height: 100vh;
  width: 100vw;
  background-color: #161616;
  padding: 20px 0;
  overflow-y: scroll;
}

.wrapper::-webkit-scrollbar {
  display: none;
}

.wrapper {
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.container {
  position: relative;
  margin: 0 400px;
}

@media (max-width: 1200px) {
  .container {
    margin: 0 300px;
  }
}

@media (max-width: 992px) {
  .container {
    margin: 0 200px;
  }
}

@media (max-width: 768px) {
  .container {
    margin: 0 30px;
  }
}

@media (max-width: 640px) {
  .container {
    margin: 0 10px;
  }
}
</style>
