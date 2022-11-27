<script>
	const now = new Date();

	let expenses = [
		{
			name: 'Food',
			cost: 6.99,
			negative: true,
			time: dateFormat(now, 'dddd, mmmm dS, yyyy, h:MM:ss TT')
		},
		{
			name: 'Pay',
			cost: 6.99,
			negative: false,
			time: dateFormat(now, 'dddd, mmmm dS, yyyy, h:MM:ss TT')
		}
	];

	const NewExpense = () => {
		let n = { name, cost, negative };
		expenses = [...expenses, n];
		name = '';
		cost = 0;
		negative = false;
	};
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
	let name;
	let cost;
	let negative;
</script>

<h2>Expense Tracker</h2>

<form on:submit|preventDefault={NewExpense}>
	<label for="">Expense</label><input bind:value={name} type="text" /><label for="">Value</label
	><input bind:value={cost} type="text" /><label for="">Positive or Negative</label><input
		bind:checked={negative}
		type="checkbox"
		name=""
		id=""
	/>
	<button>Add</button>
</form>

<table>
	<tr><th>Expense</th><th>Value</th><th>Time</th></tr>
	{#each expenses as { name, cost, negative, time }}
		<tr
			><td>{name}</td><td class:negative class:positive={!negative}
				>{#if negative}- {cost}{:else}+ {cost}{/if}</td
			><td>{time}</td></tr
		>
	{/each}
	<tr><td>Result</td><td>{result}</td><td>Right Now</td></tr>
</table>

<style>
	.negative {
		color: red;
	}
	.positive {
		color: green;
	}
</style>
