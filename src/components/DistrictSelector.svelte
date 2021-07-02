<script>
	export let districts;
	export let selectedDistrict;
</script>
<div class='container'>
	{#each districts as district}
		<button class:selected={district.name === selectedDistrict.name} on:click={() => selectedDistrict = district}>{district.name}</button>
	{/each}
</div>
<hr />
<style>
	.container{
		display: flex;
		max-width: 600px;
		margin: 0 auto;
		background-color: black;
	}
	.container button{
		flex-grow: 1;
		color: black;
		background-color: black;
		margin-right: 0;
		font-weight: bold;
		transition:  border-bottom 300ms linear ;
		z-index: 1;
		position: relative;
		border-bottom: 5px solid #383938;
	}
	button.selected{
		cursor: auto;
	}
	.container button:nth-child(1){color: #A58EE5;}
	.container button:nth-child(2){color: #BE8CD8;}
	.container button:nth-child(3){color: #CFA6D6;}
	.container button:nth-child(4){color: #CA7A9D;}
	.container button:nth-child(5){color: #FF7079;}
	.container button:nth-child(6){color: #A54C47;}
	
	.container button.selected:nth-child(1){border-bottom:5px solid #A58EE5;}
	.container button.selected:nth-child(2){border-bottom:5px solid #BE8CD8;}
	.container button.selected:nth-child(3){border-bottom:5px solid #CFA6D6;}
	.container button.selected:nth-child(4){border-bottom:5px solid #CA7A9D;}
	.container button.selected:nth-child(5){border-bottom:5px solid #FF7079;}
	.container button.selected:nth-child(6){border-bottom:5px solid #A54C47;}

	hr{
		border: 5px solid #383938;
		border-bottom: 0;
		max-width: 700px;
		margin: 0 auto 15px;
		position: relative;
		top: -6px;
		z-index: 0;
	}

</style>