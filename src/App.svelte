<script>
	let value = ''
	let tasks = []
	let lastId = tasks.length ? tasks[tasks.length - 1].id : 0

	const addTask = () => {
		lastId += 1
		const newTask = {
			id: lastId,
			label: value
		}
		tasks = [...tasks, newTask]
		value = ''
	}

	const deleteTask = (i) => {
		tasks.splice(i, 1)
		tasks = tasks
	}
</script>

<main>
	<form on:submit|preventDefault={addTask}>
		<input type="text" bind:value />
		<button type="submit">追加</button>
	</form>

	{#if tasks.length > 0}
		<ul>
	{#each tasks as task, i (task.id)}
			<li>
				{task.label}({task.id})
				<button type="button" on:click={deleteTask(i)}>削除</button>
			</li>
	{/each}
		</ul>
	{:else}
		<p>タスクがありません</p>
	{/if}
</main>
