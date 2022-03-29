<template>
  <div>
    <header>
      <h1>vue Todo with Typescript</h1>
    </header>
    <main>
      <todo-input
        :item="todoText"
        @input="updateTodoText"
        @add="addTodoItem"
      ></todo-input>
      <div>
        <ul>
          <li>아이템 1</li>
          <li>아이템 2</li>
          <li>아이템 3</li>
        </ul>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoInput from "./components/TodoInput.vue";

export default Vue.extend({
  components: { TodoInput },
  data() {
    return {
      todoText: "",
    };
  },
  methods: {
    updateTodoText(value: string) {
      this.todoText = value;
    },
    addTodoItem() {
      const value = this.todoText;
      localStorage.setItem(value, value);
      this.initTodoText();
    },
    initTodoText() {
      this.todoText = "";
    },
  },
});
</script>

<style scoped></style>
