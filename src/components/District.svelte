<script>	
	import Cause from '../components/Cause.svelte';
	
	export let district;
	
	$: penalties = district.causes.map(c => c.penalidad);
	$: maxPenalty = Math.max(...penalties);

	$: ammounts = district.causes
		.map(c => parseInt(c.monto))
		.filter(a => !isNaN(a));
	$: maxAmmount = Math.max(...ammounts);

	
</script>

{#each district.causes as cause (cause.causa)}
	<Cause cause={cause} maxPenalty={maxPenalty} maxAmmount={maxAmmount}/>
{/each}
