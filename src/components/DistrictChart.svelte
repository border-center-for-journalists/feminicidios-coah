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
	<DistrictSelector bind:selectedDistrict={selectedDistrict} districts={districts}/>
	<TypeSelector bind:selectedType={selectedType} />
	<District district={selectedDistrict} />
</div>
<style>
	.box{
		margin: 0 auto;
		max-width: 500px;
	}
</style>