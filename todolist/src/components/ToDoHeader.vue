<template>
  <div>
  <h1>Just Do It.</h1>
  <input
      type="text"
      placeholder="할 일을 입력해주세요."
      v-model="newItem"
      @keyup.enter="addNewItems"
  >

  <button @click="addNewItems">
    추가하기
  </button>
  </div>
</template>

<script>
export default {
  name: "ToDoFooter",
  data() {
    return {
    newItem : '',
    }
  },
  methods : {
    addNewItems() {
      if (this.newItem !== "") {
        this.$emit('emitAddItem', this.newItem);
        this.newItem = "";
      }
    }
  }
}
</script>

<style scoped>

</style>
