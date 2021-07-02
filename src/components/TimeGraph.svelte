<script>
	import * as rawData from '../data/deaths.json';	
	import Line from "svelte-chartjs/src/Line.svelte";

	console.log(Line);
	let dataLine = {
	    labels: [2015,2016,2017,2018,2019,2020],
	    datasets: [
	      {
	        label: "Homicidios dolosos de mujeres",
	        fill: true,
	        lineTension: 0.3,
	        backgroundColor: "rgba(164,140,230,.2)",
	        borderColor: "rgb(164,140,230)",
	        pointBorderWidth: 5,
	        pointHitRadius: 10,
	        data: [67,44,36,27,48,40]
	      },
	      {
	        label: "Carpetas iniciadas por feminicidio",
	        fill: true,
	        lineTension: 0.3,
	        backgroundColor: "rgba(218,97,82,.2)",
	        borderColor: "rgb(218,97,82)",
	        pointBorderWidth: 4,
	        pointHitRadius: 10,
	        data: [16,15,13,13,24,24]
	      }
	    ]
	  };
	let options = {
		responsive: true,
        legend: {
            labels: {
            	fontColor : 'white',
            	fontFamily : 'Aleo',
            	fontSize : 14,
            	usePointStyle : true,
            	padding:20,
            	boxWidth:10
            }
        },
		scales: {
			yAxes: [
				{
					ticks: {
						beginAtZero: true,
						fontColor:'white',
						fontFamily : 'Aleo',
					}
				}
			],

			xAxes: [
				{
					ticks: {
						fontColor:'white',
						fontFamily : 'Aleo',
					}
				}
			]
		}
	}
</script>

<h1>Homicidios dolosos de mujeres vs carpetas iniciadas por feminicidio</h1>
<div class='container'>
	<Line data={dataLine} {options} />
	<div class='notes'>
		<p class='source'>Fuente: Elaboración propia con datos entregados por la Fiscalía de Coahuila.</p>
	</div>
</div>

<style>
	.container{
		max-width: 800px;
		margin: 0 auto;
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