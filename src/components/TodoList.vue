<template>
<div>
	<div id="empty" class="list-todo" v-if="!todosList.length">
		<p id="content-empty">Empty!</p>
	</div>
	<ul v-else class="list-todo">
		<li v-for="(todo, index) in todosList" :key="index" :class="{ isDone: todo.isDone }" >
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
							<i class="fa-solid fa-pen-clip"></i>
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
	props: {
		todos: {
			type: Object
		}
	},
    data() {
        return {
            todosList: this.todos,
        };
	},
    methods: {
        destroy(index) {
            this.todosList.splice(index, 1);
        },
        updateTodo(index) {
            this.todosList[index].showFormTodo = false;
        }
    },
};
</script>
<style>
button {
	cursor: pointer;
}

.todolist {
	position: relative;
	margin: 0 auto;
	width: 700px;
	min-height: 500px;
	box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.todolist>div:first-child {
	width: 100%;
	height: 100px;
	background-color: #f763ad;
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
	white-space: normal
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
