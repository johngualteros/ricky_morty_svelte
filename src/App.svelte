<script>

	
	let page = 1;
	
	let characters = [];
	
	const getData = async () => {
		const response = await fetch(`https://rickandmortyapi.com/api/character/?page=${page}`);
		const data = await response.json();
		characters = data.results;
	}
	getData();

	const increment = () => {
		page++;
		getData();
	}
	const decrement = () => {
		page--;
		getData();
	}
</script>

<main>
	<div>
		<h1>Ricky and Morty</h1>

		<div class="container_buttons">
			<button on:click={decrement} disabled={page===1}>Previous</button>
			<button on:click={increment} disabled={page===42}>Next</button>
		</div>
		
		<div class="container_cards">
			{#each characters as character}
				<div class="card">
					<img src={character.image} alt={character.name}>
					<h2>{character.name}</h2>

					{#if character.status === "Alive"}
						<p>Status: <span class="status_alive">{character.status}</span></p>
					{/if}
					{#if character.status === "Dead"}
						<p>Status: <span class="status_dead">{character.status}</span></p>
					{/if}
					{#if character.status === "unknown"}
						<p>Status: <span class="status_unknown">{character.status}</span></p>
					{/if}
				</div>
			{/each}
		</div>
	</div>
</main>
<style>
	:global(body) {
		padding: 0;
		background-color: #000;
		margin: 0;
		font-family: -apple-system, BlinkMacSystemFont, Avenir Next, Avenir,
			Helvetica, sans-serif;
	}
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	.container_cards{
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		grid-gap: 40px;
	}
	.status_unknown{
		color: #ff3;
	}
	.status_alive{
		color: #0f0;
	}
	.status_dead{
		color: #f00;
	}
	.card {
		border: 1px solid #237bff;
		border-radius: 10px;
		padding: 20px;
	}
	.card img{
		width: 100%;
		height: auto;
	}
	.container_buttons{
		width: 100%;
		display: flex;
		justify-content: space-around;
		align-items: center;
	}
	.container_buttons button{
		padding: 10px 20px;
		background-color: rgba(0, 124, 255, 0.5);
		color: #fff;
		border: none;
		border-radius: 5px;
		cursor: pointer;
		font-weight: bold;
	}
	h1 {
		text-shadow: 
		0 0  5px #23b2ff,
		0 0  10px #23b2ff,
		0 0  20px #23b2ff,
		0 0 40px #23b2ff,
		0 0 80px #2382ff,
		0 0  90px #2382ff,
		0 0 100px #2382ff,
		0 0  110px #2382ff,
		0 0  120px #2382ff,
		0 0  140px #2382ff;
		color: #fff;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>