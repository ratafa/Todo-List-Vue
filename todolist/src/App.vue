<template>
  <Container>
    <ToDoHeader @emitAddItem="addItem"></ToDoHeader>
    <ToDoList
        :toDoItems="toDoItems"
        @emitDeleteItem="deleteItem"
    ></ToDoList>
    <ToDoFooter
        @emitClearAll="clearAll"
    ></ToDoFooter>
  </Container>
</template>

<script>
import styled from 'vue-styled-components';
import ToDoList from '@/components/ToDoList';
import ToDoHeader from '@/components/ToDoHeader';
import ToDoFooter from '@/components/ToDoFooter';

const Container = styled.div`
  padding: 20px;
`;

export default {
  name: 'App',
  data() {
    return {
      toDoItems: [],
    }
  },
  async created() {
    let itemJson = localStorage.getItem(`toDoItem`);
    if (itemJson) {
      try {
        this.toDoItems = JSON.parse(itemJson)
      } catch {
        console.log('error in LocalStorage')
      }
    }

  },
  components: {
    Container,
    ToDoHeader,
    ToDoList,
    ToDoFooter,
  },
  methods : {
    addItem(item) {
      let value = {
        itemName : item,
        isCompleted : false,
      }
      this.toDoItems.push(value);
      this.saveLocal();
    },
    deleteItem(toDoItem) {
      this.toDoItems.splice(toDoItem, 1);
      this.saveLocal();
    },
    clearAll() {
      this.toDoItems = [];
      this.saveLocal();
    },
    saveLocal() {
      localStorage.setItem('toDoItem', JSON.stringify(this.toDoItems))
    }
  }
}
</script>
