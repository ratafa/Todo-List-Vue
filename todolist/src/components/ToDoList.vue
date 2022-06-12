<template>
  <Container>
    <List
        v-for="(toDoItem) in toDoItems"
        :key="toDoItem"
        :isChecked="toDoItem.isCompleted"
    >
      <CheckBox
        type="checkbox"
        :checked=toDoItem.isCompleted
        @change="toDoItem.isCompleted = !toDoItem.isCompleted"
      ></CheckBox>
      {{toDoItem.itemName}}
    <DeleteButton @click="$emit('emitDeleteItem', toDoItem)"></DeleteButton>
    </List>
  </Container>
</template>

<script>
import styled, {css} from 'vue-styled-components';

const Container = styled.div`
  padding-top: 30px;
  display: flex;
  flex-direction: column;
  justify-content: center;
`;


const List = styled('div', {isChecked : Boolean})`
 ${({isChecked}) => isChecked && css`
  text-decoration: line-through;
 `}
`;

const CheckBox = styled.input`

`;

const DeleteButton = styled.button`
  height: 10px;
`;

export default {
  name: "TodoList",
  data() {
    return {
    }
  },
  props: ["toDoItems"],
  components : {
    Container,
    List,
    DeleteButton,
    CheckBox,
  },
  methods : {

  },
  }
</script>

<style scoped>

</style>
