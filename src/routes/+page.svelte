<script>
	import { onMount } from "svelte";
	let toggle = [false];
	const endpoint = "https://resultsapi.herokuapp.com/events/3877";
	let posts = [];

	onMount(async function() {
		const response = await fetch(endpoint);
		const data = await response.json();
		console.log(data);
		posts = data;
	})

</script>

<h1>GAA State 25 Meter Indoor Championship</h1>

<h2 on:click={() => (toggle[2] = !toggle[2])}>
	Barebow 60+ (Master 60) Men
</h2>
{#if toggle[2]}<table class="competitors">
		<thead>
			<tr>
				<th>Rank</th>
				<th>Name</th>
				<th>Target</th>
				<th>Score</th>
				<th>10s</th>
				<th>9s</th>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td>1</td>
				<td>Jim Thomas</td>
				<td>15C</td>
				<td>348</td>
				<td>3</td>
				<td>7</td>
			</tr>
			<tr on:click={() => (toggle[2167] = !toggle[2167])}>
				<td>2</td>
				<td>Andrew Henshaw</td>
				<td>16A</td>
				<td>292</td>
				<td>1</td>
				<td>4</td>
			</tr>
		</tbody>
	</table>
	{#if toggle[2167]}
		<table class="details">
			<tbody>
				<tr class="round"
					><td colspan="5">
						<table>
							<tbody>
								<tr>
									<th rowspan="2" class="round">1</th>
									<td class="arrows">8 2 M</td>
									<td class="arrows">5 1 M</td>
									<td class="arrows">5 M M</td>
									<td class="arrows"><span class="nine">9</span> 7 3</td>
									<td class="arrows">6 5 2</td>
									<td class="arrows">7 4 M</td>
									<td class="arrows">7 7 1</td>
									<td class="arrows">8 5 M</td>
									<td class="arrows">7 3 M</td>
									<td class="arrows">7 6 4</td>
									<td class="arrows">Total</td>
									<td class="arrows">Avg</td>
								</tr>
								<tr class="ends">
									<td class="end_total">10</td>
									<td class="end_total">6</td>
									<td class="end_total">5</td>
									<td class="end_total">19</td>
									<td class="end_total">13</td>
									<td class="end_total">11</td>
									<td class="end_total">15</td>
									<td class="end_total">13</td>
									<td class="end_total">10</td>
									<td class="end_total">17</td>
									<td class="end_total">119</td>
									<td class="end_total">4.0</td>
								</tr>
								<tr class="gap"><td></td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td></tr>
								<tr>
									<th rowspan="2" class="round">2</th>
									<td class="arrows">7 6 5</td>
									<td class="arrows"><span class="nine">9</span> 8 5</td>
									<td class="arrows">8 7 2</td>
									<td class="arrows">8 7 6</td>
									<td class="arrows">4 4 M</td>
									<td class="arrows"><span class="nine">9</span> 8 5</td>
									<td class="arrows"><span class="nine">9</span> 7 6</td>
									<td class="arrows"><span class="ten">10</span> 5 4</td>
									<td class="arrows">5 4 2</td>
									<td class="arrows">6 4 3</td>
									<td class="arrows">Total</td>
									<td class="arrows">Avg</td>
								</tr>
								<tr class="ends">
									<td class="end_total">18</td>
									<td class="end_total">22</td>
									<td class="end_total">17</td>
									<td class="end_total">21</td>
									<td class="end_total">8</td>
									<td class="end_total">22</td>
									<td class="end_total">22</td>
									<td class="end_total">19</td>
									<td class="end_total">11</td>
									<td class="end_total">13</td>
									<td class="end_total">173</td>
									<td class="end_total">5.8</td>
								</tr>
							</tbody>
						</table>
					</td>
				</tr>
			</tbody>
		</table>
	{/if}
{/if}

{#each posts.rps as rps}
<div>
	<p>{rps.fnm} {rps.lnm}</p>
</div>
{/each}