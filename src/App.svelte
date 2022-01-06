<script>
	import Task from './Task.svelte'

	let value = ''
	const idKey = 'svelteTodoAppId'
	const taskKey = 'svelteTodoAppTasks'
	const tempSavedTasks = localStorage.getItem(taskKey)
    let tasks = tempSavedTasks ? JSON.parse(tempSavedTasks) : []
	let lastId = localStorage.getItem(idKey)
		? Number(localStorage.getItem(idKey))
		: 0

	const addTask = () => {
		lastId += 1
		const newTask = {
			id: lastId,
			label: value
		}
		tasks = [...tasks, newTask]
		localStorage.setItem(idKey, lastId)
		localStorage.setItem(taskKey, JSON.stringify(tasks))
		value = ''
	}

	const handleEdit = (ev) => {
		tasks[ev.detail.index].label = ev.detail.label
		localStorage.setItem(taskKey, JSON.stringify(tasks))
	}

	const handleDelete = (ev) => {
		tasks.splice(ev.detail.index, 1)
		tasks = tasks
		localStorage.setItem(taskKey, JSON.stringify(tasks))
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
