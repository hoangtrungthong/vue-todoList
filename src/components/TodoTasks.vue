<template>
  <div>
	<ul class="list-todo">
		<li v-for="(todo, index) in todoTasks" :key="index" :class="{ isDone: todo.isDone }" >
			<div class="item">
				<div>
					<input v-if="!todo.showFormTodo" @click="todo.isDone = !todo.isDone" type="checkbox">
					<label v-else>Edit</label>
					<input v-if="todo.showFormTodo" v-model="todo.name" />
					<p v-else>{{ todo.name }}</p>
				</div>
				<div>
					<div v-if="!todo.showFormTodo">
						<button class="action-btn" @click="todo.showFormTodo = true">
						</button>
						<button class="action-btn" @click="destroy(index)">
							<i class="fa-solid fa-trash-can"></i>
						</button>
					</div>
					<button v-else class="btn-add" @click="updateTodo(index)">Save</button>
				</div>
			</div>
		</li>
	</ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      todoTasks: [
        { name: "asdasd", isDone: false, showFormTodo: false },
        { name: "bcd", isDone: false, showFormTodo: false },
        { name: "efg", isDone: false, showFormTodo: false },
        { name: "ghk", isDone: false, showFormTodo: false },
      ],
    };
  },
};
</script>
<style></style>
