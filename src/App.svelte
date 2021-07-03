<script>
	import DistrictChart from './components/DistrictChart.svelte';
	import SankeyChart from './components/SankeyChart.svelte';
	import TimeGraph from './components/TimeGraph.svelte';

	import queryString from 'query-string';

	const urlParams = queryString.parse(location.search);
	const table = urlParams.table ? urlParams.table : '1';
</script>

<main>
	{#if table === '1'}
		<DistrictChart />
	{:else if table === '2'}
		<TimeGraph />
	{:else if table === '3'}
		<h1>Mujeres víctimas de homicidio doloso por lugar y causa de muerte</h1>
		<SankeyChart />
	{/if}
</main>
<style>
	h1{
		text-align: center;
	}
</style>