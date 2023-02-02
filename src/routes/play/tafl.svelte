<script lang="ts">
	import { Vector } from '$lib/utils/datypes';

	const grid: number[][] = [];
	const whites = [
		[4,2],
		[4,3],
		[4,5],
		[4,6],
		[2,4],
		[3,4],
		[5,4],
		[6,4],
	]
	for (let y = 0; y < 9; y++) {
		grid[y] = [];
		for (let x = 0; x < 9; x++) {
			grid[y][x] = 0;
		}
	}
	for (const pos of whites) {
		const x = pos[0]
		const y = pos[1]
		grid[y][x]=1
	}
	let selected: Vector | null = null;
	function click(x: number, y: number) {
		if (selected == null && grid[y][x]!=0) {
			selected = new Vector(x, y);
		} else {
			if (grid[y][x] == 0 && (selected.y == y || selected.x == x)) {
				grid[y][x] = grid[selected.y][selected.x];
				grid[selected.y][selected.x]=0
				selected=null
			}
		}
	}
	console.log(grid);
</script>

<table>
	{#each grid as row, cellY}
		<tr>
			{#each row as cell, cellX}
				<td
					class:selected={selected?.x == cellX && selected?.y == cellY}
					on:click={() => click(cellX, cellY)}>
					<!-- {cellX}:{cellY} -->
					{cell}
					</td
				>
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
	td.selected {
		background-color: red;
	}
	tr {
		display: flex;
	}
	table {
		border: 1px black solid;
		width: max-content;
	}
</style>
