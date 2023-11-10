<script>
	import { fade, fly } from 'svelte/transition';

	let todos = [];
	let newTodo = '';

	function loadTodos() {
		const storedTodos = localStorage.getItem('todos');
		if (storedTodos) {
			todos = JSON.parse(storedTodos);
		}
	}

	if (typeof localStorage !== 'undefined') {
		loadTodos();
	}

	function saveTodos() {
		localStorage.setItem('todos', JSON.stringify(todos));
	}

	function addTodo() {
		if (newTodo !== '' && newTodo[0] !== ' ') {
			todos = [...todos, { text: newTodo, completed: false }];
			newTodo = '';
			saveTodos();
		}
	}

	function removeTodo(index) {
		todos.splice(index, 1);
		todos = todos;
		saveTodos();
	}

	function editTodo(index) {
		const newText = prompt('Edit teh todo: ', todos[index].text);
		if (newText !== null && newText !== '' && newText !== ' ') {
			todos[index].text = newText;
			todos = [...todos];
			saveTodos();
		}
	}
	function toggleCompleted(index) {
		todos[index].completed = !todos[index].completed;
		todos = [...todos];
		saveTodos();
	}

	function handleKeyPress(event) {
		if (event.key === 'Enter') {
			addTodo();
		}
	}
</script>

<div class="todoCard">
	<h1>Todo List</h1>
	<div class="input-section">
		<input
			class="input-text"
			type="text"
			bind:value={newTodo}
			placeholder="Add a new task"
			on:keydown={handleKeyPress}
		/>
		<button class="todo-add-btn" on:click={addTodo}>+</button>
	</div>
	<ul>
		{#each todos as todo, index}
			<div class="li-box" in:fly={{ x: 50, duration: 1000 }} out:fade>
				<input id={todo.id} class="ui-checkbox" bind:checked={todo.completed} type="checkbox" />
				<span class="li-text" class:checked={todo.completed}>{todo.text}</span>
				<span class="edit-btn" on:click={() => editTodo(index)}>✏️</span>
				<span class="delete-btn" on:click={() => removeTodo(index)}>❌</span>
			</div>
		{/each}
	</ul>
</div>

<style>
	h1 {
		text-align: center;
		font-family: 'Edu TAS Beginner', cursive;
		font-size: 3.5rem;
		margin-bottom: 50px;
		letter-spacing: 3px;
	}

	.todoCard {
		background-color: rgb(50, 50, 20, 0.2);
		width: 700px;
		height: 600px;
		box-shadow: rgba(0, 0, 0, 0.1) 0px 10px 15px -3px, rgba(0, 0, 0, 0.05) 0px 4px 6px -2px;
		border-bottom-left-radius: 10px;
		border-bottom-right-radius: 10px;
	}

	@media screen and (max-width: 768px) {
		.todoCard {
			width: 100%;
			height: auto;
			border-radius: 0;
			box-shadow: none;
		}
		.li-text {
			max-width: 250px;
			word-wrap: break-word;
		}
	}

	.input-section {
		display: flex;
		align-items: center;
		justify-content: center;
		margin-bottom: 50px;
	}

	.li-box {
		display: flex;
		align-items: flex-start;
	}

	.li-text {
		font-size: 1.3rem;
		border-bottom: 1px dotted;
		max-width: 500px;
		word-wrap: break-word;
		margin-bottom: 20px;
		font-family: 'Edu TAS Beginner', cursive;
	}

	input {
		line-height: 25px;
		background-color: transparent;
		border-left: none;
		border-right: none;
		border-top: none;
	}

	.input-text {
		font-family: 'Edu TAS Beginner', cursive;
		font-size: 1.3rem;
	}
	.todo-add-btn {
		background-color: transparent;
		border-radius: 50%;
		margin-left: 10px;
		width: 30px;
		height: 30px;
		font-size: 1.3rem;
		border-color: black;
	}

	.todo-add-btn:hover {
		border-color: green;
		color: green;
	}

	.edit-btn {
		margin-left: 10px;
		margin-right: 10px;
	}

	.todo-add-btn,
	.edit-btn,
	.delete-btn {
		cursor: pointer;
	}

	.checked {
		text-decoration: line-through;
	}
</style>
