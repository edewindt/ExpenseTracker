<script>
	let expenses = [{ name: 'Food', cost: 6.99, negative: true }];
</script>

<h2>Expense Tracker</h2>

<table>
	{#each expenses as { name, cost, negative }}
		<tr><td>{name}</td><td>{cost}</td><td>{negative}</td></tr>
	{/each}
</table>
