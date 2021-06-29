<script>
	export let selectedType;
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
	<button class={type.class}><span class="material-icons">{type.icon}</span>{type.name}</button>
	{/each}
</div>
<style>
	.container{
		display: flex;
	}
	button{
		flex: 1 1 0px;
	}
	button.oral{
		background-color: #006E81;
	}

	button.abbr{
		background-color: #2F4858;
	}
	button .material-icons{
		margin-right: 6px;
		position: relative;
		top: 5px;
	}
</style>