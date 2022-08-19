<template>
  <div class="todolist">
    <div></div>
    <div></div>
    <div class="main">
      <!-- <todo-add @items="todo" />
      <TodoList :todos="todos" /> -->
      <todo-task #="todosTask">
        <ul class="list-todo">
          <li v-for="(todos, index) in todosTask" :key="index">
            <div
              v-for="(todo, index) in todos"
              :key="index"
              :class="{ isDone: todo.isDone }"
            >
              <h1>
              <div v-if="!todo.isDone" class="item">
                <div>
                  <input
                    v-if="!todo.showFormTodo"
                    @click="completed(todo)"
                    type="checkbox"
                  />
                  <label v-else>Edit</label>
                  <input v-if="todo.showFormTodo" v-model="todo.name" />
                  <p v-else>{{ todo.name }}</p>
                </div>
                <div>
                  <div v-if="!todo.showFormTodo">
                    <button
                      class="action-btn"
                      @click="todo.showFormTodo = true"
                    ></button>
                    <button class="action-btn" @click="destroy(index)">
                      <i class="fa-solid fa-trash-can"></i>
                    </button>
                  </div>
                  <button v-else class="btn-add" @click="updateTodo(index)">
                    Save
                  </button>
                </div>
              </div>
              </h1>
            </div>
          </li>
        </ul>
      </todo-task>
      <ul class="list-todo complete">
        <h3>
          <li v-for="(todo, index) in todosCompleted" :key="index">
            <h4>
            <div v-if="todo.isDone" class="item">
              <div>
                <input
                  v-if="!todo.showFormTodo"
                  @click="completed()"
                  type="checkbox"
                />
                <label v-else>Edit</label>
                <input v-if="todo.showFormTodo" v-model="todo.name" />
                <p v-else>{{ todo.name }}</p>
              </div>
              <div>
                <div v-if="!todo.showFormTodo">
                  <button
                    class="action-btn"
                    @click="todo.showFormTodo = true"
                  ></button>
                  <button class="action-btn" @click="destroy(index)">
                    <i class="fa-solid fa-trash-can"></i>
                  </button>
                </div>
                <button v-else class="btn-add" @click="updateTodo(index)">
                  Save
                </button>
              </div>
            </div>
            </h4>
          </li>
        </h3>
      </ul>
      <div style="margin-top: 60px">
        <button @click="selectComponent('todo-complete')">complete</button>
        <button @click="selectComponent('todo-tasks')">task</button>
      </div>
      <component :is="selectedComponent"></component>
    </div>
  </div>
</template>
<script>
import TodoTask from "./TodoTask.vue";
import TodoTasks from "./TodoTasks.vue";
import TodoComplete from "./TodoComplete.vue";
export default {
  data() {
    return {
      todosCompleted: [],
      selectedComponent: "todo-tasks"
    };
  },
  methods: {
    destroy(index) {
      this.todosList.splice(index, 1);
    },
    updateTodo(index) {
      this.todosList[index].showFormTodo = false;
    },
    completed(todo) {
      todo.isDone = true;
      this.todosCompleted.unshift(todo)
    },
    selectComponent(cpn) {
      this.selectedComponent = cpn
    }
  },
  components: { TodoTask, TodoTasks, TodoComplete },
};
</script>
<style>
button {
  cursor: pointer;
}

h1 {
  background: yellow;
}

h4 {
  background: green;
}

h4 p {
  color: white;
  font-weight: 100;
}

.todolist {
  position: relative;
  margin: 0 auto;
  width: 700px;
  min-height: 500px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.todolist > div:first-child {
  width: 100%;
  height: 100px;
  background-color: #f763ad;
}
.complete {
  margin-top: 150px !important;
}
.main {
  position: absolute;
  left: 0;
  right: 0;
  top: 12%;
  width: 400px;
  margin: 0 auto;
  background: white;
  border-radius: 10px;
}

.main > div:first-child {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  height: 100px;
  padding: 10px;
  text-align: left;
  border-radius: 10px;
}

.main label {
  font-weight: bold;
}

input {
  outline: none;
  border: 1px solid #ccc;
  padding: 8px 15px;
  border-radius: 10px;
}

.btn-add {
  background: #f763ad;
  border: none;
  padding: 8px 15px;
  border-radius: 10px;
  color: white;
  font-weight: bold;
}

.form-group {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
}

.form-group input {
  width: 80%;
}

.error {
  padding: 5px 0;
  color: red;
  font-style: italic;
  font-size: 14px;
}

.list-todo {
  border: 1px solid #ccc;
  border-radius: 10px;
  margin-top: 40px;
  width: 100%;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

ul li {
  border-top: 2px solid #ccc;
  list-style: none;
  padding: 10px;
}

ul li:first-child {
  border: none;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}

.item div:first-child {
  display: flex;
  align-items: center;
  gap: 10px;
}

p {
  color: rgb(86, 86, 86);
  word-wrap: break-word;
  white-space: normal;
}

.action-btn {
  width: 20px;
  border: none;
  background: white;
  color: #f763ad;
}

#empty {
  height: 100px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

#content-empty {
  margin-top: 40px;
}

.isDone {
  background: greenyellow;
}

.isDone .action-btn {
  background: greenyellow;
}
</style>
