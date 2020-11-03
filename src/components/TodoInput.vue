<template>
  <div class="inputWrapper">
    <h2>Add todo</h2>

    <form @submit.prevent="handleSubmit" class="todo_wrapper" action="">
      <input
        v-model="input"
        class="todoInput"
        :class="{ invalid: $v.input.$dirty && !$v.input.required }"
        type="text"
        placeholder="Enter todo"
      />
      <button class="addBtn" type="submit">Add</button>
    </form>
    <span class="required" v-if="$v.input.$dirty && !$v.input.required">Field is required</span>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";

export default {
  name: "todo-input",
  data: () => ({
    input: "",
  }),
  methods: {
    handleSubmit() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }

      this.$emit("addTodo", {
        title: this.input,
        date: Date.now(),
      });
      this.input = "";
      this.$v.input.$reset();
    },
  },
  validations: {
    input: { required },
  },
};
</script>

<style scoped>
.inputWrapper {
  position: relative;
  margin-bottom: 20px;
  background-color: #202020;
  padding: 10px;
  border-radius: 15px;
  color: white;
}

.inputWrapper h2 {
  text-align: center;
  margin-bottom: 20px;
}

.todo_wrapper {
  display: flex;
  align-items: center;
  flex-direction: row;
  justify-content: space-around;
}

.todoInput {
  width: 80%;
  outline: none;
  background-color: #202020;
  border: none;
  padding: 2px 0;
  color: white;
  border-bottom: 1px solid #444444;
}

.addBtn {
  padding: 5px 10px;
  border-radius: 10px;
  border: none;
  background-color: rgb(0, 117, 252);
  color: #ffffff;
  font-size: 15px;
  font-weight: bold;
  letter-spacing: 1px;
  outline: none;
  cursor: pointer;
}

.invalid {
  border-bottom-color: rgb(141, 1, 1);
}
.required {
    margin-left: 10px;
    text-align: center;
    font-size: 12px;
}
</style>