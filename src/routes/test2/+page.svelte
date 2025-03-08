<script lang="ts">
	const TIMES = 20; //stroopwafel
	const GROUP = 5;
</script>

<table>
	<thead>
		<tr>
			{#each { length: TIMES } as _, i}
				<th><code>{i.toString().padEnd(2, '_')}_</code></th>
			{/each}
		</tr>
	</thead>
	<tbody>
		<tr>
			{#each { length: TIMES } as _, i}
				<td class="">{Math.floor(i / GROUP)}</td>
			{/each}
		</tr>
		<tr>
			{#each { length: TIMES } as _, i}
				<td class="">{Math.floor(i / GROUP) % 2}</td>
			{/each}
		</tr>
		<tr>
			{#each { length: TIMES } as _, i}
				<td class="">{i % 2}</td>
			{/each}
		</tr>
		<tr>
			{#each { length: TIMES } as _, i}
				<td class="">{+(i % 2 === Math.floor(i / GROUP) % 2)}</td>
			{/each}
		</tr>
	</tbody>
</table>
