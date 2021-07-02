<script>
	import * as rawData from '../data/deaths.json';	
	import Line from "svelte-chartjs/src/Line.svelte";

	let dataLine = {
	    labels: [2015,2016,2017,2018,2019,2020],
	    datasets: [
	      {
	        label: "Homicidios dolosos a mujeres",
	        fill: true,
	        lineTension: 0.3,
	        backgroundColor: "rgba(225, 204,230, .3)",
	        borderColor: "rgb(205, 130, 158)",
	        pointBorderWidth: 5,
	        pointHitRadius: 10,
	        data: [67,44,36,27,48,40]
	      },
	      {
	        label: "Carpetas iniciadas por feminicidio",
	        fill: true,
	        lineTension: 0.3,
	        backgroundColor: "rgba(184, 185, 210, .3)",
	        borderColor: "rgb(35, 26, 136)",
	        pointBorderWidth: 5,
	        pointHitRadius: 10,
	        data: [16,15,13,13,24,24]
	      }
	    ]
	  };
	let options = {
		responsive: true,
		plugins: {
			legend: {
				labels: {
					// This more specific font property overrides the global property
					font: {
						size: 30
					}
				}
			}
		}
	};
</script>

<h1>Homicidios dolosos a mujeres vs carpetas iniciadas por feminicídio</h1>
<div class='container'>
	<Line data={dataLine} options={options} />
</div>

<style>
	.container{
		max-width: 800px;
		margin: 0 auto;
	}
</style>