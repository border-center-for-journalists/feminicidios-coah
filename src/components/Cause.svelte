<script>
	export let cause;
	export let maxPenalty;
	export let maxAmmount;

	const currencyFormater = new Intl.NumberFormat('es-MX', { style: 'currency', currency: 'MXN' })
	const penaltyPct = cause.penalidad / maxPenalty * 100;
	const ammountPct = Number.isFinite(maxAmmount) ? cause.monto / maxAmmount * 100 : 0;
	const ammount = !isNaN(cause.monto) ? currencyFormater.format(cause.monto) : cause.monto; 
	const typeIcon = cause.tipo === 'Juicio oral' ? 'gavel' : 'timer';
	const typeClass = cause.tipo === 'Juicio oral' ? 'oral' : 'abbr';
</script>
<div class='container {typeClass}'>
	<div class='type cell'><span class="material-icons">{typeIcon}</span></div>
	<div class='cause cell'>
		{cause.causa}
		{#if cause.notas} <sup>{cause.noteNum}</sup>{/if}
	</div>
	<div class='range'>
		<div class='indicator' style='width: {penaltyPct}%'></div>
		<p>{cause.penalidad} años</p>
	</div>
	<div class='range'>
		<div class='indicator' style='width: {ammountPct}%'></div>
		<p>
			{ammount}
			{#if ammount === 'Ilíquida'}*{/if}
		</p>
	</div>
</div>


<style>
	p{
		margin: 0;
	}
	sup{font-size: 11px}
	.container{	
		display: flex;
		margin-bottom: 1px;
	}
	.container.oral div{
		background-color: white;
		color: black;
	}
	.container.abbr div{
		background-color: black;
	}
	.cell{
		padding: 0 10px 0;
		margin-right: 1px;
		color: white;
	}
	.cell .material-icons{
		margin-top: 4px;
	}
	.cause{
		width: 87px;
		height: 33px;
		overflow: hidden;
  		text-overflow: ellipsis;
  		white-space: nowrap;
  		line-height: 33px;
	}

	.type{
		font-size: 13px;
	}	

	.range{
		height: 33px;
		position: relative;
		margin-right: 1px;
		flex: 1 1 0px;
		background-color: black!important;

	}
	.range p{
		width: 100%;
		color: white;
		display: block;
		position: relative;
		font-size: 13px;
		line-height: 38px;
		padding-left: 8px;
	}
	.container .range .indicator{
		position: absolute;
		left: 0;
		top:  0;
		height: 100%;
		background-color: #A48AE4;
	}
	
</style>
