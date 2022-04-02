<template>
  <li>
    <span class="item" :class="todoItemClass" @click="toggleItem">{{
      todoItem.title
    }}</span>
    <button @click="removeItem">삭제</button>
  </li>
</template>

<script lang="ts">
import { Todo } from "@/App.vue";
import Vue, { PropType } from "vue";

export default Vue.extend({
  props: {
    todoItem: Object as PropType<Todo>, //이 객체의 타입은 title, done이 들어가는  Todo 인터페이스이다.
    index: Number,
  },
  computed: {
    todoItemClass(): string | null {
      //필히 타입정의를 해주어야함.
      return this.todoItem.done ? "complete" : null;
    },
  },
  methods: {
    toggleItem() {
      this.$emit("toggle", this.todoItem, this.index);
    },
    removeItem() {
      this.$emit("remove", this.index); //remove할때마다 뭘 삭제했는지 알 수 있음.
    },
  },
  /**
 * 
 * version1 ->
 * todoItem: String,
 * 
 * vue.runtime.esm.js?c320:619 [Vue warn]: Invalid prop: type check failed for prop "todoItem". Expected String, got Object 

    found in

    ---> <TodoListItem> at src/components/TodoListItem.vue
          <App> at src/App.vue
            <Root>
 *
 * version2 ->
 *  todoItem: Object as PropType<Todo>,
 *  vue 내부적으로 PropType 제공. PropType 은 제네릭을 받음.
 *  원하는 타입을 (여기선 <Todo> )을 넘길 수 있음.
 * 
 */

  //저렇게 하면 테스트 범주에 해당하지 않은건 안건들여야하는데, 테스트하기 복잡해짐.
  //"$emit('delete')"을 바로 html안에 쓸 수도 있지만.(코드량도 줄어들고)
  //그럼에도 따로 method 로 빼는 것이 좋음.
});
</script>

<style scoped>
.item {
  cursor: pointer;
}
.complete {
  text-decoration: line-through;
}
</style>
