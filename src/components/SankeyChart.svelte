<script>
	import * as rawData from '../data/deaths.json';
	import {Chart, LinearScale} from 'chart.js';
	import {SankeyController, Flow} from 'chartjs-chart-sankey';
	import { onMount } from 'svelte';

	const deaths = rawData.default;

	const places = deaths.map(d => d.place)
		.filter((d,i,a) => a.indexOf(d) === i);

	const stats = {}; 
	let dataset = [];
	
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
		let datapoints = place.causes.map(cause => {
			return {
				from : place.place,
				to : cause.cause,
				flow : cause.count
			}
		})
		dataset.push.apply(dataset, datapoints);
	}
	Chart.register(LinearScale, SankeyController, Flow);
	
	var colors2 = ['#00D4FF','#FEEF00','#FF8EFF','#1F1C0C','#9B915C','#FF84AE'];
	var assigned = {};
	function c2(name) {
	  return assigned[name] || (assigned[name] = colors2[Object.keys(assigned).length % colors2.length]);
	}
	let data = {
		datasets: [{
			data: dataset,
			colorMode: 'gradient', 
			colorFrom: (c) => c2(c.dataset.data[c.dataIndex].from),
			colorTo: (c) => c2(c.dataset.data[c.dataIndex].to),
			labels : true,
			borderWidth: 1,
			borderColor: 'black',
			/* optional labels */
			/*labels: {
				a: 'Label A',
				b: 'Label B',
				c: 'Label C'
			}*/
		}]
	}

	onMount(async () => {
		var ctx = document.getElementById("chart").getContext("2d");
		const chart = new Chart(ctx, {
		  type: 'sankey',
		  data : data,
		});
	});
</script>

<canvas id="chart"></canvas>

<style>

</style>
