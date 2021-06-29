<script>
	export let districts;
	export let selectedDistrict;
</script>
<div class='container'>
	{#each districts as district}
		<button class:selected={district.name === selectedDistrict.name} on:click={() => selectedDistrict = district}>{district.name}</button>
	{/each}
</div>
<style>
	.container{
		display: flex;
	}
	.container button{
		flex-grow: 1;
	}

</style>