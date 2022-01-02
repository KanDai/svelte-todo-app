<script>
	const todos = [
		{ id: 0, label: 'a'},
		{ id: 1, label: 'b'}
	]
</script>

<main>
{#if todos.length > 0}
	<ul>
{#each todos as todo, i (todo.id)}
		<li>{i + 1} {todo.label}</li>
{/each}
	</ul>
{:else}
	<p>todoがありません</p>
{/if}
</main>
