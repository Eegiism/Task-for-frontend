<script>
	export let items;

	let searchBar = "";
	let filteredItem = [];

	// Searching by title
	$: {
		if(searchBar) {
			filteredItem = items.filter(item => item.title.includes(searchBar))
		} else {
			filteredItem = [...items]
		}
	}

	//Searching by tab 
	function handleFilter(parametr){
		if(parametr!== 'all') {
			filteredItem = items.filter(item => item.tags.includes(parametr));
		} else {
			filteredItem = [...items]
		}
	}	
</script>

<style>
	.panel-tabs ul {
		display: flex;
   		flex-direction:row;
	}
</style>


<nav class="panel">
	<p class="panel-heading">
	  Repositories
	</p>
	<div class="panel-block">
	  <p class="control has-icons-left">
		<input class="input" type="text" bind:value = {searchBar} placeholder="Search">
		<span class="icon is-left">
		  <i class="fas fa-search" aria-hidden="true"></i>
		</span>
	  </p>
	</div>
	<div class="panel-tabs">
		  <!-- svelte-ignore a11y-missing-attribute -->
		<ul> 
			<li class="is-active"> 	<a target="_blank" on:click = { ()=> handleFilter('all')  } > All </a> </li>
			<li> <a  target="_blank" on:click = { ()=> handleFilter('public')  }> Public</a> </li>
			<li> <a  target="_blank" on:click = { ()=> handleFilter('private')  } > Private</a> </li>
			<li> <a  target="_blank" on:click = { ()=> handleFilter('sources')  } > Sources</a> </li>
			<li> <a  target="_blank" on:click = { ()=> handleFilter('forks')  } > Forks</a> </li>
		</ul>
	</div>
	  <!-- svelte-ignore a11y-missing-attribute -->
	  <ul>
			{#each filteredItem as item}
				<li>
					<a class="panel-block is-active">
						{#if item.icon === 'book'}
							<span class="panel-icon">
								<i class="fas fa-book"></i>
							</span>
							{item.title}
						{:else}
							<span class="panel-icon">
								<i class="fas fa-code-branch"></i>
							</span>
							{item.title}
						{/if}
					</a>
				</li>
			{/each}
		</ul>

	<div class="panel-block">
	  <button class="button is-link is-outlined is-fullwidth" on:click = { ()=> handleFilter('all') }>
		Reset all filters
	  </button>
	</div>
  </nav>