<script>
	let todos = [];
	let newTodo = '';

	function addTodo() {
		if (newTodo.trim() === '') {
			return;
		}
		todos = [...todos, { text: newTodo, completed: false }];
		newTodo = '';
	}

	function removeTodo(index) {
		todos = todos.filter((_, i) => i !== index);
	}

	function toggleCompleted(index) {
		todos[index].completed = !todos[index].completed;
		todos = [...todos];
	}
</script>

<h1>Todos</h1>

<div class="todoCard">
	<input type="text" bind:value={newTodo} placeholder="Add a new todo" />
	<button on:click={addTodo}>Add</button>
	<ul>
		{#each todos as todo, index (todo.text)}
			<li class:todo.completed={todo.completed}>
				<input
					type="checkbox"
					bind:checked={todo.completed}
					on:change={() => toggleCompleted(index)}
				/>
				{todo.text}
				<button on:click={() => removeTodo(index)}>Remove</button>
			</li>
		{/each}
	</ul>
</div>

<style>
	h1 {
		text-align: center;
	}
	.todoCard {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-content: center;
		background-color: grey;
		height: 500px;
		width: 500px;
	}

	input {
		width: 50%;
		padding: 2px;
		margin-bottom: 10px;
	}

	li {
		list-style-type: none;
		display: flex;
		align-items: center;
		margin: 5px 0;
		padding: 5px;
		border: 1px solid #ccc;
	}

	button {
		width: 25%;
		padding: 2px;
	}

	.completed {
		text-decoration: line-through;
	}
</style>
