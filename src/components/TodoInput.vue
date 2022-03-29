<template>
  <div>
    <label for="todo-input">오늘 할 일 : </label>
    <input id="todo-input" type="text" :value="item" @input="handleInput" />
    <button @click="addTodo" type="button">추가</button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  //props: ["item"],
  props: {
    item: {
      type: String,
      required: true,
    },
  },
  methods: {
    handleInput(event: InputEvent) {
      //no implicity has an any type
      //"strict": true,
      //"noImplicitAny": true,
      //위 둘 중 하나라도 true를 하면 noImplictAny가 true가 됨 (기본은 noImplictAny: false)
      //console.log(event); => console을 찍을 경우 InputEvent로 타입이 찍혀서 타입을 알아낼 수 있다.

      //강의 소제목 : 인풋 컴포넌트 프롭스 속성 유효성 검사 및 타입 정의 -
      //object is possiblt null이 나온다면 null이 아니라는 것을 보장해야함.

      /** 방법 1 : 하나하나 if문을 대입해준다.
       * if(!event.target){
       *   return;
       * }
       *
       */
      /** 방법 2 : 이벤트 type을 명시적으로 선언해준다. */
      const eventTarget = event.target as HTMLInputElement;
      this.$emit("input", eventTarget.value); //여기서 보낸 값이 string이기에 App파일의 updateTodoText도 바꿔줌.
    },
    addTodo() {
      this.$emit("add");
    },
  },
});
</script>

<style scoped></style>
