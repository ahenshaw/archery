<script>
// @ts-nocheck

	import { onMount } from "svelte";
	import Scores from "./Scores.svelte";
	let toggle = [false];
	const event_url = "https://resultsapi.herokuapp.com/events/3877";
	const scores_url = "https://resultsapi.herokuapp.com/events/3877/scores";
	/**
	 * @type {never[]}
	 */
	let event = [];
	let scores = [];
	let competitors;

	onMount(async function() {
		const scores_response = await fetch(scores_url);
		const scores_data = await scores_response.json();
		console.log(scores_data);
		scores = scores_data.ars;

		const event_response = await fetch(event_url);
		const event_data = await event_response.json();
		// console.log(event_data);
		event = event_data;
		competitors = event.rps;

	})

	function compute_scores(arrows) {
		let total = 0;
		let tens = 0;
		let nines = 0;
		for (const ch of arrows) {
			if (ch == 'T') {total += 10; tens += 1;}
			else if (ch == 'M') {}
			else {total += Number(ch)}
			if (ch == '9') {nines += 1}
		}
		return [total, tens, nines];
	}


</script>

<h1>{event.tnm}</h1>
<h2>{event.tlc} | {event.tdt}</h2>
{#each event.cgs as division}
	{#if division.ars.length > 0}
		<h2 class="division" on:click={() => (toggle[division.dor] = !toggle[division.dor])}>
			{division.nm}
		</h2>
		{#if toggle[division.dor]}
			<table class="competitors">
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
				{#each division.ars as archers}
					{@const archer = competitors[archers.aid]}
					{@const arrows = scores[archers.aid]}
					{@const score = compute_scores(arrows)}
					<tr on:click={() => (toggle[archers.aid] = !toggle[archers.aid])}>
						<td>-</td>
						<td>{archer.fnm}
							{archer.lnm}
						</td>
						<td>{archer.tgt[0]}</td>
						<td>{score[0]}</td>
						<td>{score[1]}</td>
						<td>{score[2]}</td>
					</tr>
					{#if toggle[archers.aid]}
						<tr>
							<td colspan=6><Scores arrows={arrows} /></td>
						</tr>
					{/if}
				{/each}
				</tbody>
			</table>
		{/if}

	{/if}
{/each}
<!-- <h2 on:click={() => (toggle[2] = !toggle[2])}>
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

{#each event.rps as rps}
<div>
	<p>{rps.fnm} {rps.lnm}</p>
</div>
{/each}

<h2 on:click={() => (toggle[3] = !toggle[3])}>
	Barebow Senior Men
</h2>
{#if toggle[3]}<table class="competitors">
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
		</tbody>
	</table>
{/if} -->
