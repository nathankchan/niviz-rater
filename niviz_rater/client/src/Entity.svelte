<!--
	Each entity component represents a single object that is to be
	QC'd by the user.

	Properties:
		- Entity: Object storing information on entity that is
			represented by this view
		- rating: Rating for entity
		- pass: 1 if pass, 0 if fail
		- comment: Current entities comment?
-->

<script>

	import { createEventDispatcher } from 'svelte';

	// Props for placement
	export let entity;
	const dispatch = createEventDispatcher();

	function handleClick(){
		dispatch(
			'message', {
				id: entity.id
			}
		)
	}

	function getClass(e){
		
		if (e == null){
			return "column is-2 notification is-dark"
		}

		let modifier;
		if (e.failed == true){
			modifier = "is-danger"
		} else if (e.failed == false){
			modifier = "is-success"
		} else {
			modifier = ""
		}
		return `column is-2 box is-clickable notification ${modifier}`
	}

	let entityClass;
	$:entityClass = getClass(entity);


</script>

<div on:click={(entity) ? handleClick : ''} class='{entityClass}'>
	{#if entity}
		<strong>{entity.name}</strong>
	{/if}
</div>

<style>
	.column.box{
		-webkit-filter: brightness(100%);
	}

	.column.box:hover{
		-webkit-filter: brightness(90%);
		transition: all 0.30s ease;
	}

	.notification:not(:last-child){
		margin-bottom:0;
	}
</style>
