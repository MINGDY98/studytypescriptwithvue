<template>
  <div>
    <header>
      <h1>vue Todo with Typescript</h1>
    </header>
    <main>
      <TodoInput
        :item="todoText"
        @input="updateTodoText"
        @add="addTodoItem"
      ></TodoInput>
      <div>
        <ul>
          <TodoListItem
            v-for="(todoItem, index) in todoItems"
            :key="index"
            :index="index"
            :todoItem="todoItem"
            @remove="removeTodoItem"
          ></TodoListItem>
          <!-- <li>아이템 1</li>
          <li>아이템 2</li>
          <li>아이템 3</li> -->
        </ul>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoInput from "./components/TodoInput.vue";
import TodoListItem from "./components/TodoListItem.vue";

const STORAGE_KEY = "vue-todo-ts-v1";
const storage = {
  save(todoItems: any[]) {
    //직렬화 : 배열=> string 변환
    const parsed = JSON.stringify(todoItems);
    localStorage.setItem(STORAGE_KEY, parsed);
  },
  fetch() {
    const todoItems = localStorage.getItem(STORAGE_KEY) || "[]";
    const result = JSON.parse(todoItems);
    /**
     * Argument of type 'string | never[]' is not assignable to parameter of type 'string'.
  Type 'never[]' is not assignable to type 'string
     * 타입 오류가 나는 이유.
     * JSON.parse의 첫번째 파라메터가 string이라고 되어있기 때문 (parse에 마우스 올리면 알수있음)
     * 그래서 JSON.parse안에 들어갈 것은 string이거나 string 하위 타입이여야함
     * []를 '[]'로 바꿈으로서 문제해결
     *
     */
    return result;
  },
};
export default Vue.extend({
  components: { TodoInput, TodoListItem },
  data() {
    return {
      todoText: "",
      todoItems: [] as any[],
    };
  },
  methods: {
    updateTodoText(value: string) {
      this.todoText = value;
    },
    addTodoItem() {
      const value = this.todoText;
      //localStorage.setItem(value, value);
      this.todoItems.push(value);
      storage.save(this.todoItems);
      this.initTodoText();
    },
    initTodoText() {
      this.todoText = "";
    },
    fetchTodoItems() {
      this.todoItems = storage.fetch();
      //todoItems가 never[]로되어있는데 그 이유는 data에 []만 초기화시키고 타입을 지정안해서!
    },
    removeTodoItem(index: number) {
      console.log("remove", index);
      this.todoItems.splice(index, 1);
      storage.save(this.todoItems);
    },
  },
  created() {
    this.fetchTodoItems();
  },
});
</script>

<style scoped></style>
