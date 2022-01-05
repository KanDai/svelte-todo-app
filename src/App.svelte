<script>
	import Task from './Task.svelte';

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

	const handleEdit = (ev) => tasks[ev.detail.index].label = ev.detail.label

	const handleDelete = (ev) => {
		tasks.splice(ev.detail.index, 1)
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
			<Task {...task} index={i} on:edit={handleEdit} on:delete={handleDelete} />
	{/each}
		</ul>
	{:else}
		<p>タスクがありません</p>
	{/if}
</main>
