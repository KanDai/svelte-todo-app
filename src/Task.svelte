<script>
	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()

	export let index
	export let id
	export let label
	export let isDone
	let isEditable = false
	let tempLabel = label

	const cnacelEdit = () => {
		isEditable = false
		tempLabel = label
	}

	const editTask = () => {
		dispatch('edit', {
			index,
			label: tempLabel
		});
		isEditable = false
	}

	const deleteTask = (index) => {
		dispatch('delete', {
			index
		});
	}

	const doneTask = (ev) => {
		dispatch('done', {
			index,
			checked: ev.target.checked
		});
	}
</script>

<li>
	{#if isEditable === true}
		<form on:submit|preventDefault={editTask}>
			<input type="text" bind:value={tempLabel}>
			<button type="button" on:click={cnacelEdit}>キャンセル</button>
			<button type="submit">決定</button>
		</form>
	{:else}
		<input type="checkbox" bind:checked={isDone} on:change={doneTask}>
		<span data-id={id}>{label}</span>
		<button type="button" on:click={() => isEditable = true}>編集</button>
		<button type="button" on:click={() => deleteTask(index)}>削除</button>
	{/if}
</li>