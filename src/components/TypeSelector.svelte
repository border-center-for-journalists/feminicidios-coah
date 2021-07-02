<script>
	let types = 
	[
		{
			name: 'Procedimiento abreviado',
			icon: 'timer',
			class: 'abbr'
		},
		{
			name: 'Juicio oral',
			icon: 'gavel',
			class: 'oral'
		}
	];
</script>

<div class='container'>
	{#each types as type}
		<div class={type.class}><span class="material-icons">{type.icon}</span>{type.name}</div>
	{/each}
</div>
<style>
	.container{
		display: flex;
		margin-bottom: 20px;
	}
	.container div{
		flex: 1 1 0px;
		background-color: black;
		color: white;
		border-radius: 20px;
		border: 2px solid white;
		line-height: 27px;
		padding-bottom: 2px;
		text-align: center;
	}
	.container div.oral{
		background-color: white;
		color: black;
		border: 2px solid black;
		margin-left: 10px;
	}

	.container div .material-icons{
		margin-right: 6px;
		position: relative;
		top: 5px;
	}
</style>