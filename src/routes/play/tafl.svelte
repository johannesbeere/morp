<script lang="ts">
	import { Vector } from '$lib/utils/datypes';

	const grid: number[][] = [];
	const peons = [
		[1, 4,2],
		[1, 4,3],
		[1, 4,5],
		[1, 4,6],
		[1, 2,4],
		[1, 3,4],
		[1, 5,4],
		[1, 6,4],
		[2, 3,0],
		[2, 4,0],
		[2, 5,0],
		[2, 4,1],
		[2, 0,3],
		[2, 0,4],
		[2, 0,5],
		[2, 1,4],
		[2, 3,8],
		[2, 4,8],
		[2, 5,8],
		[2, 4,7],
		[2, 8,3],
		[2, 8,4],
		[2, 8,5],
		[2, 7,4],
		[3, 4,4],

	]
	for (let y = 0; y < 9; y++) {
		grid[y] = [];
		for (let x = 0; x < 9; x++) {
			grid[y][x] = 0;
		}
	}
	for (const pos of peons) {
		const x = pos[1]
		const y = pos[2]
		grid[y][x]=pos[0]
	}
	let selected: Vector | null = null;
	function click(x: number, y: number) {
		if (selected == null && grid[y][x]!=0) {
			selected = new Vector(x, y);
		} else if(selected) {
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
					class="type-{cell}"
					on:click={() => click(cellX, cellY)}>
					<!-- {cellX}:{cellY} -->
				</td>
			{/each}
		</tr>
	{/each}
</table>

<style>
	td {
		/* width: 50px;
		height: 50px; */
		box-sizing: border-box;
		flex: 1;
		aspect-ratio: 1/1;
		border: 1px rgb(24, 23, 23) solid;
		display: flex;
		align-items: center;
		justify-content: center;
		/* background-color: grey; */
		user-select: none;
	}
	td.selected {
		/* border-color: red;
		border-width: 5px; */
		box-shadow: inset 0px 0px 0px 5px #f00;
	}
	tr {
		display: flex;
		/* width: 100%; */
	}
	table {
		border: 1px black solid;
		/* width: max-content; */
		width: 90vmin;
		aspect-ratio: 1/1;
		margin: auto;
	}
	.type-1{
		background-color: white;
	}
	.type-3{
		background-color: yellow;
	}
	.type-2{
		background-color: black;
	}
</style>
