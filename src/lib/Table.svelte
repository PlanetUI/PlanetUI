<script lang="ts">
	export let component: any;
	export let heads: string[] = [];
	export let rows: any[] = [];
	export let search: string = '';
	export let limit: number = 5;
	export let page: number = 1;
	export let url: string = '';

	let data: any[] = rows;
	let totalPage: number = 4;

	let limitList: any[] = [
		{ id: 1, text: 5, value: 5 },
		{ id: 2, text: 10, value: 10 },
		{ id: 3, text: 25, value: 25 },
		{ id: 4, text: 50, value: 50 },
		{ id: 5, text: 100, value: 100 }
	];

	let selected: any;

	$: total = data.length;
	$: isCeil = total % limit;
	$: totalPage = isCeil > 0 ? Math.ceil(total / limit) : Math.floor(total / limit);
	function filterData() {
		page = 1;
		data = rows.filter((row) => {
			let found = false;
			for (let i = 0; i < row.length; i++) {
				if (row[i].toString().toLowerCase().includes(search.toLowerCase())) {
					found = true;
					break;
				}
			}
			return found;
		});
	}
</script>

<label for="limit">limit: </label>
<select
	name="limit"
	bind:value={selected}
	on:change={() => {
		(page = 1), (limit = selected.value);
	}}
	required
>
	{#each limitList as lm}
		<option value={lm}>{lm.text}</option>
	{/each}
</select>

<input type="text" bind:value={search} on:keyup={filterData} placeholder="Search" />
<table>
	<thead>
		<tr>
			{#each heads as head}
				<th>{head}</th>
			{/each}
		</tr>
	</thead>
	<tbody>
		{#each data as row, index}
			{#if page * limit > index && index >= (page - 1) * limit}
				<tr>
					{#each row as cell}
						{#if cell.html}
							<td>{@html cell.html}</td>
						{:else if cell.svelte}
							<td>
								<svelte:component this={component} {index} />
							</td>
						{:else}
							<td>{cell}</td>
						{/if}
					{/each}
				</tr>
			{/if}
		{/each}
	</tbody>
</table>
<br />

{#each Array(totalPage) as _, i}
	<button
		on:click={() => {
			page = i + 1;
		}}>{i + 1}</button
	>
{/each}

<br />

limit: {limit}<br />
page: {page}<br />
total: {total}<br />
url: {url}<br />
search: {search}<br />
