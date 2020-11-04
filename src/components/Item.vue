<template>
  <v-container class="d-flex">
    <v-checkbox v-model="todo.isChecked"></v-checkbox>
    <v-list-item-content>
        <v-list-item-title v-text="todo.title" :class="todo.isChecked ? 'isChecked' : ''"></v-list-item-title>
    </v-list-item-content>
    <v-list-item-action>
      <v-btn icon @click="pressIconDelete()">
        <v-icon color="red">mdi-delete</v-icon>
      </v-btn>
    </v-list-item-action>
  </v-container>
</template>

<script>
import Todo from "@/models/Todo";

export default {
  name: "Item",
  props: {
    todo: Todo,
    index: Number,
    removeTodo: Function,
    checkedTodo: Function
  },
  methods: {
    pressIconDelete(){
      this.removeTodo(this.todo);
    }
  }
}
</script>

<style scoped>
.isChecked{
  text-decoration:line-through;
}
</style>