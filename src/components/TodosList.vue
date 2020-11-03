<template>
  <div class="">
    <div v-for="todo in reverseTodos" :key="todo.id" class="todoWrapper">
      <div class="top">
        <span>{{ todo.date | dateFilter("datetime") }}</span>
        <button @click="() => onClick(todo.id)" class="close-btn">
          <span>&#10005;</span>
        </button>
      </div>
      <div class="titleWrapper">
        <span>{{ todo.title }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todos",
  props: ["todos"],
  computed: {
    reverseTodos() {
      return [...this.todos].reverse();
    },
  },
  methods: {
    onClick(id) {
      this.$emit("remove-todo", id);
    },
  },
  filters: {
    dateFilter(value, format = "date") {
      const options = {};

      if (format.includes("date")) {
        options.day = "2-digit";
        options.month = "long";
        options.year = "numeric";
      }

      if (format.includes("time")) {
        options.hour = "2-digit";
        options.minute = "2-digit";
        options.second = "2-digit";
      }

      const locale = "uk-UA";
      return new Intl.DateTimeFormat(locale, options).format(new Date(value));
    },
  },
};
</script>

<style scoped>
.todoWrapper {
  display: flex;
  flex-direction: column;
  color: white;
  background-color: #202020;
  padding: 15px;
  border-radius: 20px;
  white-space: pre-wrap;
  overflow-wrap: break-word;
  word-wrap: break-word;
}
.todoWrapper + .todoWrapper {
  margin-top: 10px;
}

.top {
  display: flex;
  justify-content: space-between;
}

.close-btn {
  color: white;
  border: none;
  background-color: #202020;
  cursor: pointer;
  outline: none;
}
.titleWrapper {
  margin-top: 10px;
}
</style>