<script>
	export let places;
	export let selectedPlace;
	var colors = ['#7a81e9','#a58ce4','#c68ce4','#f57fb4','#fd7777','#db3636'];
	const color = index => colors[index % colors.length];
	function selectPlace(place){
		selectedPlace = selectedPlace === place ? false : place;
	}
</script>
<div class='container'>
	{#each places as place , i}
		<button style='color:{color(i)}' class:selected={place === selectedPlace} on:click={() => selectPlace(place)}>{place}</button>
	{/each}
</div>
<style>
	button.selected{color: white!important}
	button.selected:nth-child(1){background-color: #7a81e9 }
	button.selected:nth-child(2){background-color: #a58ce4 }
	button.selected:nth-child(3){background-color: #c68ce4 }
	button.selected:nth-child(4){background-color: #f57fb4 }
	button.selected:nth-child(5){background-color: #fd7777 }
	button.selected:nth-child(6){background-color: #db3636 }
	button.selected:nth-child(7){background-color: #7a81e9 }
	button.selected:nth-child(8){background-color: #a58ce4 }
	button.selected:nth-child(9){background-color: #c68ce4 }
	button.selected:nth-child(10){background-color: #f57fb4 }
	button.selected:nth-child(11){background-color: #fd7777 }
	button.selected:nth-child(12){background-color: #db3636 }
	button.selected:nth-child(13){background-color: #7a81e9 }
	button.selected:nth-child(14){background-color: #a58ce4 }
	.container{
		max-width: 800px;
		margin: auto;
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		margin-bottom: 10px;
	}
	button{
		flex-grow: 1;
		color: white;
		background-color: black;
		margin-right: 1px;
		transition:  background-color 200ms linear ;
	}
</style>