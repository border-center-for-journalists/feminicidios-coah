<script>
	import DistrictChart from './components/DistrictChart.svelte';
	import SankeyChart from './components/SankeyChart.svelte';
	import TimeGraph from './components/TimeGraph.svelte';
</script>

<main>
	<h1>Carpetas con resolución por feminicídio</h1>
	<DistrictChart />
	<h1>Homicidios dolosos a mujeres vs carpetas iniciadas por feminicídio</h1>
	<TimeGraph />
	<h1>Homicidios a mujeres por lugar y causa de muerte</h1>
	<SankeyChart />
</main>
<style>
	h1{
		text-align: center;
	}
</style>