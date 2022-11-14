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

	function clearList(){
		choicesList = []
	}
</script>

<svelte:head>
	<title>Option Helper</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section class="flex items-center flex-col my-10">
	
	<div class="card w-96 bg-secondary text-primary-content">
		<div class="card-body">
			<label class="px-7 text-xl my-10 text-primary">Add Some Choices:
				<br />
				<input class="input input-bordered input-success text-white w-full max-w-xs px-2 my-1" bind:value={newItem} type="text">
			</label>
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

<!-- Put this part before </body> tag -->
<!-- <input type="checkbox" id="my-modal-4" class="modal-toggle" />
<label for="my-modal-4" class="modal cursor-pointer">
  <label class="modal-box relative" for="">
    <h3 class="text-lg font-bold">Congratulations random Internet user!</h3>
    <p class="py-4">What?!?!</p>
  </label>
</label> -->

</section>
