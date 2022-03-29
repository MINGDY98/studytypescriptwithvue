<template>
  <div>
    <label for="todo-input">오늘 할 일 : </label>
    <input id="todo-input" type="text" :value="item" @input="handleInput" />
    <button @click="addTodo" type="button">add</button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: ["item"],
  methods: {
    handleInput(event: any) {
      //no implicity has an any type
      //"strict": true,
      //"noImplicitAny": true,
      //위 둘 중 하나라도 true를 하면 noImplictAny가 true가 됨 (기본은 noImplictAny: false)
      event.target.value;
      this.$emit("input", event.target.value);
    },
    addTodo() {
      console.log("add");
    },
  },
});
</script>

<style scoped></style>
