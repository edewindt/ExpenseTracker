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

	const getResult = () => {
		let total = 0;
		for (let i = 0; i < expenses.length; i++) {
			if (expenses[i].negative === true) {
				total = total - expenses[i].cost;
			} else {
				total = total + expenses[i].cost;
			}
		}
		return total;
	};
	let result = getResult();
</script>

<h2>Expense Tracker</h2>

<table>
	<tr><th>Expense</th><th>Value</th></tr>
	{#each expenses as { name, cost, negative, time }}
		<tr><td>{name}</td><td>{cost}</td><td>{time}</td></tr>
	{/each}
	<tr><td>Result</td><td>{result}</td></tr>
</table>

<style>
</style>
