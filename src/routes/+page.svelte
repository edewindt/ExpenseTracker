<script>
	const now = new Date();

	let expenses = [
		{
			name: 'Food',
			cost: 6.99,
			negative: true,
			time: dateFormat(now, 'dddd, mmmm dS, yyyy, h:MM:ss TT')
		}
	];
	import dateFormat, { masks } from 'dateformat';
</script>

<h2>Expense Tracker</h2>

<table>
	<tr><th>Expense</th><th>Value</th></tr>
	{#each expenses as { name, cost, negative, time }}
		<tr><td>{name}</td><td>{cost}</td><td>{time}</td></tr>
	{/each}
</table>

<style>
</style>
