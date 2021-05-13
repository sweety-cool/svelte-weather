<script>
	import { TextInput, Tile, Button } from "carbon-components-svelte";
	const API_KEY = "0fb038fb61b72dc5ae3e7f192ffb6f14";

	// STATE
	let CITY = "";
	let DATA;
	// FUNCTIONS
	function getData() {
		const url = `https://api.openweathermap.org/data/2.5/weather?q=${CITY}&appid=${API_KEY}`;
		fetch(url)
			.then((r) => r.json())
			.then((data) => {
				console.log(data);
				DATA = data;
			});
	}

	function convertTemp(temp) {
		return Math.round(temp - 273.15);
	}
</script>

<div class="container">
	<h3 class="center header">Weather Info ☁</h3>
	<br />
	<p class="center">By Sweety</p>
	<p class="center">13-05-2021</p>
	<br /> <br />
	<!-- DATA BINDING -->
	<TextInput bind:value={CITY} placeholder=" Enter City..." />

	<!-- ON CLICK HANDLER -->
	<br />
	<Button on:click={getData}>SEARCH CITY</Button>

	<br />

	{#if DATA}
		<Tile>
			<h3 style="text-align: center;">
				Temp: {convertTemp(DATA.main.temp)}℃
			</h3>
		</Tile>

		<br />
		<Tile class="center">
			<h4>Name: {DATA.name}</h4>
			<p>Description:{DATA.weather[0].description}</p>
			<p>Country: {DATA.sys.country}</p>
		</Tile>

		<br />
		<Tile class="center">
			<p>Temp min:{convertTemp(DATA.main.temp_min)}℃</p>
			<p>Temp max:{convertTemp(DATA.main.temp_max)}℃</p>
			<p>pressure:{DATA.main.pressure}pa</p>
		</Tile>
	{/if}
</div>
