<script>
	let value = ''
	let todos = []
	let lastId = todos.length ? todos[todos.length - 1].id : 0

	const addTodo = () => {
		lastId += 1
		const newTodo = {
			id: lastId,
			label: value
		}
		todos = [...todos, newTodo]
		value = ''
	}
</script>

<main>
	<form on:submit|preventDefault={addTodo}>
		<input type="text" bind:value />
		<button type="submit">追加</button>
	</form>

	{#if todos.length > 0}
		<ul>
	{#each todos as todo (todo.id)}
			<li>{todo.label}({todo.id})</li>
	{/each}
		</ul>
	{:else}
		<p>todoがありません</p>
	{/if}
</main>
