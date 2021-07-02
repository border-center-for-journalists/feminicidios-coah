<script>
	import * as causes from '../data/procedimientos.json';
	import District from '../components/District.svelte';
	import DistrictSelector from '../components/DistrictSelector.svelte';
	import TypeSelector from '../components/TypeSelector.svelte';

	const districts = causes.default
		.map( p => p.distrito)
		.filter((d,i,a) => a.indexOf(d) === i)
		.map(d => {
			return {
				name : d,
				causes : causes.default.filter(p => p.distrito === d)
			}
		});	
	let selectedDistrict =  districts[0];
	let selectedType;
</script>
<div class='box'>
	<h1>Carpetas con resolución por feminicidio</h1>
	<p class='explainer'>La siguiente tabla muestra las <b>44 resoluciones </b> por feminicidio dictadas por el Poder Judicial del Estado de Coahuila. Se puede navegar la tabla haciendo clic en cada distrito para ver los datos de esa localidad. </p>
	<DistrictSelector bind:selectedDistrict={selectedDistrict} districts={districts}/>
	<section>
		<TypeSelector bind:selectedType={selectedType} />
		<District district={selectedDistrict} />
	</section>
</div>
<style>

	.box{
		margin: 0 auto;
		max-width: 800px;
		background-color: black;
		border-radius: 15px;
	}
	section{
		max-width: 500px;
		margin: 0 auto;
	}
</style>