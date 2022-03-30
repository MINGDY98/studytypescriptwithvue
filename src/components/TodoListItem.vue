<template>
  <li>
    <span>{{ todoItem }}</span>
    <button @click="removeItem">삭제</button>
  </li>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    todoItem: String,
    index: Number,
  },
  //저렇게 하면 테스트 범주에 해당하지 않은건 안건들여야하는데, 테스트하기 복잡해짐.
  //"$emit('delete')"을 바로 html안에 쓸 수도 있지만.(코드량도 줄어들고)
  //그럼에도 따로 method 로 빼는 것이 좋음.

  methods: {
    removeItem() {
      this.$emit("remove", this.index); //remove할때마다 뭘 삭제했는지 알 수 있음.
    },
  },
});
</script>

<style scoped></style>
