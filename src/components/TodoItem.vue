<template>
  <div class="todolist">
    <div></div>
    <div></div>
    <div class="main">
      <todo-add @items="todo" />
      <TodoList :todos="todos" />
    </div>
  </div>
</template>
<script>
import TodoAdd from './TodoAdd.vue';
import TodoList from './TodoList.vue';
export default {
    data() {
        return {
            todos: []
        };
    },
    methods: {
        todo(item) {
                this.todos.unshift(item);
            }
    },
    components: { TodoList, TodoAdd }
};
</script>
<style></style>
