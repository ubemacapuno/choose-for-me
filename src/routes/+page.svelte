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
	<title>Option Helper</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section class="flex items-center flex-col my-10">
	<label class="text-xl my-10">Add Some Options:
		<br />
		<input class="px-2 my-1" bind:value={newItem} type="text">
	</label>

	<button class="w-28 btn-secondary btn p-3 my-2" on:click={addToList}>Add</button>
	{#if choicesList.length > 1}
		<button class="w-28 btn btn-accent my-2" on:click={choose}>
			Random!
		</button>
	{/if}


	<div class="py-7">
		{#each choicesList as item, index}
			<p class="py-2">{item.option}
				<span class="pl-4" on:click={() => removeFromList(index)} aria-hidden="true">🗑️</span>
			</p>
		{/each} 
	</div>


</section>
