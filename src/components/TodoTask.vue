<template>
  <div>
    <todo-add @items="todo" />
    <slot :todosTask="todos"></slot>
  </div>
</template>
<script>
import TodoAdd from './TodoAdd.vue';
export default {
  components: { TodoAdd },
  data() {
    return {
      todos: [],
    };
  },

  methods: {
    todo(item) {
      this.todos.unshift(item);
    },
  },
};
</script>
<style></style>
