<script>
	let newItem = '';
	let choicesList = [];
	let randomChoice = () => Math.floor(Math.random()*(choicesList.length))

	function addToList() {
		choicesList = [...choicesList, {option: newItem}];
		newItem = '';
	}
	
	function removeFromList(index) {
		choicesList.splice(index, 1)
		choicesList = choicesList;
    }
	
	function choose(){
		alert(choicesList[randomChoice()].option)
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<label>Add Some Options:
		<br />
		<input bind:value={newItem} type="text">
	</label>

	<button on:click={addToList}>Add</button>


	{#each choicesList as item, index}
		<p>{item.option}
			<span on:click={() => removeFromList(index)} aria-hidden="true">❌</span>
		</p>
		
	{/each} 

	{#if choicesList.length > 1}
		<button on:click={choose}>
			Random!
		</button>
	{/if}
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}
</style>
