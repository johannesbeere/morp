<script>
	const grid = [];
	for (let y = 0; y < 9; y++) {
		grid[y] = [];
		for (let x = 0; x < 9; x++) {
			grid[y][x] = 0;
		}
	}

	console.log(grid);
</script>

<table>
	{#each grid as row}
		<tr>
			{#each row as cell}
				<td>{cell}</td>
			{/each}
		</tr>
	{/each}
</table>

<style>
	td {
		width: 50px;
		height: 50px;
		border: 1px black solid;
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: white;
		user-select: none;
	}

	tr {
		display: flex;
	}
	table {
		border: 1px black solid;
		width: max-content;
	}
</style>
