<script>
	import { fly } from 'svelte/transition';

	let answer = ''
	let newItem = '';
	let answerVisibility = false
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
		answer = (choicesList[randomChoice()].option)
		answerVisibility = true
	}

	function clearList(){
		choicesList = []
		answer = ''
		answerVisibility = false
	}
</script>

<svelte:head>
	<title>Choose For Me</title>
	<meta name="Are you indecisive on something? Add in some options and the app will randomly choose something!" content="SvelteKit app" />
</svelte:head>

<section class="flex items-center flex-col my-10">

	<div class="card w-96 bg-secondary text-primary-content">
		<div class="card-body">
			<label class="px-7 text-xl my-10 text-primary">Add Some Choices:
				<br />
				<input class="input input-bordered input-success text-white w-full max-w-xs px-2 my-1" bind:value={newItem} type="text">
			</label>

			{#if answerVisibility === true && choicesList.length > 0}
				<h2 class="pb-7 text-xl text-fuchsia-300 text-center">We've chosen <span class="font-bold text-error">{answer}</span>!</h2>
			{/if}

			<div class="flex justify-center">
				<button class="mx-2 w-28 btn-primary btn p-3 my-2 order-2" on:click={addToList}>Add</button>
				{#if choicesList.length > 1}
					<button class="mx-2 w-28 btn btn-accent my-2 order-3" on:click={choose}>
						Choose!
					</button>
					<!-- <label for="my-modal-4" class="w-28 btn btn-accent my-2">Random</label> -->
					<button class="mx-2 w-28 btn btn-warning my-2 order-1" on:click={clearList}>
						Clear
					</button>
				{/if}
			</div>
		</div>
	</div>

	<div class="py-7">
		{#each choicesList as item, index}
			<p class="py-2">{item.option}
				<span class="pl-4" on:click={() => removeFromList(index)} aria-hidden="true">🗑️</span>
			</p>
		{/each} 
	</div>
</section>
