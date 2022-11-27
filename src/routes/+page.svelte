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
		let n = {
			name,
			cost,
			negative,
			time: dateFormat(new Date(), 'dddd, mmmm dS, yyyy, h:MM:ss TT')
		};
		expenses = [...expenses, n];
		name = '';
		cost = 0;
		negative = false;
	};
	import dateFormat, { masks } from 'dateformat';

	const getResult = (a) => {
		let total = 0;
		for (let i = 0; i < a.length; i++) {
			if (a[i].negative === true) {
				total = total - a[i].cost;
			} else {
				total = parseFloat(total) + parseFloat(a[i].cost);
			}
		}
		return total;
	};
	$: result = getResult(expenses).toFixed(2);
	let name;
	let cost;
	let negative;
	let time;
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
				>{#if negative}- ${cost}{:else}+ ${cost}{/if}</td
			><td>{time}</td></tr
		>
	{/each}
	<tr><td>Result</td><td>${result}</td><td>Right Now</td></tr>
</table>

<style>
	.negative {
		color: red;
	}
	.positive {
		color: green;
	}
</style>
