<script>
	import * as rawData from '../data/deaths.json';
	import PlaceSelector from '../components/PlaceSelector.svelte';
	import {Chart, LinearScale, registerables} from 'chart.js';
	import {SankeyController, Flow} from 'chartjs-chart-sankey';
	import { onMount } from 'svelte';

	const deaths = rawData.default;
	const places = deaths.map(d => d.place).filter((d,i,a) => a.indexOf(d) === i);
	const causes = deaths.map(d => d.cause).filter((d,i,a) => a.indexOf(d) === i);

	var colors = ['#7a81e9','#a58ce4','#c68ce4','#f57fb4','#fd7777','#db3636'];
	const color = index => colors[index % colors.length];

	let stats = {}; 
	let chart;
	let dataset = [];
	let selectedPlace = false;
	
	for(let i = 0;i<places.length;i++){
		stats[places[i]] = {
			place : places[i],
			causes : {}
		}
	};

	for(let i = 0; i < deaths.length; i++){
		if (typeof stats[deaths[i].place].causes[deaths[i].cause] !== 'undefined'){
			stats[deaths[i].place].causes[deaths[i].cause].count++;
		}else{
			stats[deaths[i].place].causes[deaths[i].cause] = {
				cause : deaths[i].cause,
				count : 1
			};
		}
	}

	let statsArray = Object.values(stats).map(stat => {
		stat.causes = Object.values(stat.causes);
		return stat;
	});

	for(let i = 0 ; i < statsArray.length ; i++){
		let place = statsArray[i];
		let datapoints = place.causes.map((cause,j) => {
			return {
				from : place.place,
				to : cause.cause,
				flow : cause.count,
				colorFrom : color(places.indexOf(place.place)),
				colorTo : color(causes.indexOf(cause.cause))
			}
		})
		dataset.push.apply(dataset, datapoints);
	}
	Chart.register(...registerables,LinearScale, SankeyController, Flow);
	Chart.defaults.font.size = 14;
	Chart.defaults.font.family = 'Aleo';
	
	let data = {
		datasets: [{
			data: dataset,
			colorMode: 'gradient', 
			colorFrom: (c) => c.dataset.data[c.dataIndex].colorFrom,
			colorTo: (c) => c.dataset.data[c.dataIndex].colorTo,
			labels : true,
			borderWidth: 1,
			borderColor: 'black',
			color:'white',
		}]
	}
	function updateData(selectedPlace){
		if(chart){
			const filteredData = selectedPlace ? dataset.filter(node => node.from === selectedPlace) : dataset;
			data.datasets[0].data = filteredData;
			chart.data = data;
			chart.update();
		}
	}
	$: updateData(selectedPlace);

	onMount(async () => {
		var ctx = document.getElementById("chart").getContext("2d");
		chart = new Chart(ctx, {
		  type: 'sankey',
		  data : data, 
		  options: {
    		plugins: {
      			tooltip: {
        			enabled: true,
        			external: undefined
      			}
    	  	}
    	  }
		});
	});
</script>
<PlaceSelector places={places} bind:selectedPlace={selectedPlace}/>
<div class='container'>
	<canvas id="chart"></canvas>

	
</div>
<div class='notes'>
		<p class='source'>Fuente: Elaboración propia con datos entregados por la Fiscalía de Coahuila.</p>
	</div>
<style>
	canvas{
		max-width: 800px;
	}
	.container{
		display: flex;
  		justify-content: center;
  		padding-bottom: 20px;
	}
	.notes{
		max-width: 800px;
		margin: 10px auto;
	}
	.notes p{
		color: white;
		margin: 4px 0;
	}
	.notes .source{
		color: #aaa;
		text-align: right;
		font-style: italic;
	}
</style>
