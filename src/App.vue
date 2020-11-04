<template>
  <v-app>
    <v-main>
      <HelloWorld/>
      <Todo></Todo>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import Todo from "@/components/Todo";

export default {
  name: 'App',

  components: {
    Todo,
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
