<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <v-text-field :label="setPlaceHolder" v-on:keyup.enter="addTodo" v-model="todoInput"></v-text-field>
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col class="mb-4">

        <v-card tile>
              <v-list-item v-for="(todo, index) in getTodoList" :key="index" :class="todo.isChecked ? 'active' : ''">
                <Item :todo="todo" :index="index" :remove-todo="removeTodo"></Item>
              </v-list-item>
        </v-card>
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col class="mb-4">
        <v-btn :disabled="this.classBtn[0]" @click="displayAll">Toutes les taches</v-btn>
        <v-btn :disabled="this.classBtn[1]" @click="displayActive">Active</v-btn>
        <v-btn :disabled="this.classBtn[2]" @click="displayComplete">Complête</v-btn>
      </v-col>
    </v-row>

  </v-container>
</template>

<script>

import Item from "@/components/Item";
import Todo from "@/models/Todo";

export default {
  name: "Todo",
  components: { Item },
  data: () => ({
    todoList: [],
    todoInput: '',
    classBtn: [true, false, false]
  }),
  methods:{
    addTodo() {
      this.todoList.push(new Todo(this.todoInput));
      this.todoInput = '';
    },
    displayAll() {
      this.classBtn = [true, false, false];
    },
    displayActive() {
      this.classBtn = [false, true, false];
    },
    displayComplete() {
      this.classBtn = [false, false, true];
    },
    removeTodo(todo) {
        this.todoList.splice(this.todoList.indexOf(todo), 1);
    }
  },
  computed: {
    setPlaceHolder() {
      return this.todoList.length === 0 ? 'Une tache à faire ?' : 'Une autre tache à ajouter';
    },
    getTodoList() {
      if(this.classBtn[0] === true){
        return this.todoList;
      }else if (this.classBtn[1] === true){
        return this.todoList.filter((elt => !elt.isChecked));
      }else{
        return this.todoList.filter((elt => elt.isChecked));
      }
    }
  }
}
</script>

<style scoped>
.active{
  background-color: rgba(49, 180, 4, 0.2);
}
</style>