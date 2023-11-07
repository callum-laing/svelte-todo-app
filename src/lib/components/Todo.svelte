<script>
	let todos = [];
	let newTodo = '';

	function addTodo() {
		todos = [...todos, { text: newTodo, completed: false }];
		newTodo = '';
	}

	function removeTodo(index) {
		todos.splice(index, 1);
		todos = todos;
	}

	function toggleCompleted(index) {
		todos[index].completed = !todos[index].completed;
		todos = [...todos];
	}
</script>

<div class="todoCard">
	<h1>Todo List</h1>
	<input type="text" bind:value={newTodo} placeholder="Add a new todo" />
	<button on:click={addTodo}>Add</button>
	<ul>
		{#each todos as todo, index}
			<div class="li-box">
				<input class="ui-checkbox" bind:checked={todo.completed} type="checkbox" />
				<span class="li-text" class:checked={todo.completed}>{todo.text}</span>
				<button class="delete-button" on:click={() => removeTodo(index)}>❌</button>
			</div>
		{/each}
	</ul>
</div>

<style>
	h1 {
		text-align: center;
		font-family: 'Caveat', cursive;
		font-size: 3rem;
	}

	.li-text {
		font-size: 1.5rem;
		padding-bottom: 10px;
	}

	input {
		line-height: 25px;
	}

	.li-box {
		display: flex;
		justify-content: center;
	}
	.todoCard {
		background-color: rgb(50, 50, 20, 0.2);
		width: 700px;
		height: 600px;
		box-shadow: rgba(0, 0, 0, 0.1) 0px 10px 15px -3px, rgba(0, 0, 0, 0.05) 0px 4px 6px -2px;
		border-bottom-left-radius: 10px;
		border-bottom-right-radius: 10px;
	}

	.checked {
		text-decoration: line-through;
	}

	.delete-button {
		background-color: transparent;
		border: transparent;
		cursor: pointer;
	}
	/* checkbox settings 👇 */

	.ui-checkbox {
		--primary-color: #1677ff;
		--secondary-color: #fff;
		--primary-hover-color: #4096ff;
		/* checkbox */
		--checkbox-diameter: 20px;
		--checkbox-border-radius: 5px;
		--checkbox-border-color: #d9d9d9;
		--checkbox-border-width: 1px;
		--checkbox-border-style: solid;
		/* checkmark */
		--checkmark-size: 1.2;
	}

	.ui-checkbox,
	.ui-checkbox *,
	.ui-checkbox *::before,
	.ui-checkbox *::after {
		-webkit-box-sizing: border-box;
		box-sizing: border-box;
	}

	.ui-checkbox {
		-webkit-appearance: none;
		-moz-appearance: none;
		appearance: none;
		width: var(--checkbox-diameter);
		height: var(--checkbox-diameter);
		border-radius: var(--checkbox-border-radius);
		background: var(--secondary-color);
		border: var(--checkbox-border-width) var(--checkbox-border-style) var(--checkbox-border-color);
		-webkit-transition: all 0.3s;
		-o-transition: all 0.3s;
		transition: all 0.3s;
		cursor: pointer;
		position: relative;
	}

	.ui-checkbox::after {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		-webkit-box-shadow: 0 0 0 calc(var(--checkbox-diameter) / 2.5) var(--primary-color);
		box-shadow: 0 0 0 calc(var(--checkbox-diameter) / 2.5) var(--primary-color);
		border-radius: inherit;
		opacity: 0;
		-webkit-transition: all 0.5s cubic-bezier(0.12, 0.4, 0.29, 1.46);
		-o-transition: all 0.5s cubic-bezier(0.12, 0.4, 0.29, 1.46);
		transition: all 0.5s cubic-bezier(0.12, 0.4, 0.29, 1.46);
	}

	.ui-checkbox::before {
		top: 40%;
		left: 50%;
		content: '';
		position: absolute;
		width: 4px;
		height: 7px;
		border-right: 2px solid var(--secondary-color);
		border-bottom: 2px solid var(--secondary-color);
		-webkit-transform: translate(-50%, -50%) rotate(45deg) scale(0);
		-ms-transform: translate(-50%, -50%) rotate(45deg) scale(0);
		transform: translate(-50%, -50%) rotate(45deg) scale(0);
		opacity: 0;
		-webkit-transition: all 0.1s cubic-bezier(0.71, -0.46, 0.88, 0.6), opacity 0.1s;
		-o-transition: all 0.1s cubic-bezier(0.71, -0.46, 0.88, 0.6), opacity 0.1s;
		transition: all 0.1s cubic-bezier(0.71, -0.46, 0.88, 0.6), opacity 0.1s;
	}

	/* actions */

	.ui-checkbox:hover {
		border-color: var(--primary-color);
	}

	.ui-checkbox:checked {
		background: var(--primary-color);
		border-color: transparent;
	}

	.ui-checkbox:checked::before {
		opacity: 1;
		-webkit-transform: translate(-50%, -50%) rotate(45deg) scale(var(--checkmark-size));
		-ms-transform: translate(-50%, -50%) rotate(45deg) scale(var(--checkmark-size));
		transform: translate(-50%, -50%) rotate(45deg) scale(var(--checkmark-size));
		-webkit-transition: all 0.2s cubic-bezier(0.12, 0.4, 0.29, 1.46) 0.1s;
		-o-transition: all 0.2s cubic-bezier(0.12, 0.4, 0.29, 1.46) 0.1s;
		transition: all 0.2s cubic-bezier(0.12, 0.4, 0.29, 1.46) 0.1s;
	}

	.ui-checkbox:active:not(:checked)::after {
		-webkit-transition: none;
		-o-transition: none;
		-webkit-box-shadow: none;
		box-shadow: none;
		transition: none;
		opacity: 1;
	}
</style>
