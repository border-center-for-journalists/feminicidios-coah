<script>	
	import Cause from '../components/Cause.svelte';
	
	export let district;
	
	$: penalties = district.causes.map(c => c.penalidad);
	$: maxPenalty = Math.max(...penalties);

	$: ammounts = district.causes
		.map(c => parseInt(c.monto))
		.filter(a => !isNaN(a));
	$: maxAmmount = Math.max(...ammounts);

	$: notes = district.causes.filter(c => c.notas !== '').map(c => c.notas);
	$: causes = district.causes.map(c => {
		c.noteNum = notes.indexOf(c.notas) + 1;
		return c;
	});
	
</script>
	<div class='container'>
		<div class='cell type'></div>
		<div class='cell cause'>Causa Penal</div>
		<div class='cell range'>Penalidad Dictada</div>
		<div class='cell range'>Monto reparación del daño</div>
		
	</div>
	{#each causes as cause (cause.causa)}
		<Cause cause={cause} maxPenalty={maxPenalty} maxAmmount={maxAmmount}/>
	{/each}
	<div class='notes'>
		<p class='source'>Fuente: Elaboración propia con datos entregados por el Poder Judicial del Estado de Coahuila </p>
		<p >* no se precisó algún monto al momento de que se dictó sentencia </p>
		{#each notes as note, i}
			<p>{i+1}. {note}</p>
		{/each}
	</div>

<style>
	.notes{
		color: white;
		text-align: left;
		margin-top:15px;
		padding-top: 8px;
		text-size: 12px;
		border-top: 1px solid #444;
	}
	.notes p{
		margin: 4px 0;
	}
	.notes .source{
		color: #aaa;
		text-align: left;
		font-style: italic;
	}
	.container{	
		display: flex;
		margin-bottom: 1px;
	}
	.container .cell{
		color: black;
		background-color: white;
		font-size: 13px;
		padding: 7px 0 5px 5px;
		margin-right: 1px;
	}
	.cell.type{
		width: 44px;
		padding: 7px 0 5px 0;
	}
	.cell.cause{
		width: 102px;
	}
	.cell.range{
		flex: 1 1 0px;
	}
</style>