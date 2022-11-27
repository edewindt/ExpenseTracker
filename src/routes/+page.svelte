<script>
	const now = new Date();
	onMount(() => {
		let x = localStorage.getItem('expenses');
		x = JSON.parse(x);
		if (x) {
			expenses = x;
		}
	});

	let expenses = [];

	const NewExpense = () => {
		let n = {
			name,
			cost,
			negative,
			time: dateFormat(new Date(), 'dddd, mmmm dS, yyyy, h:MM:ss TT')
		};
		expenses = [...expenses, n];
		name = '';
		cost = null;
		negative = false;
		localStorage.clear();
		localStorage.setItem('expenses', JSON.stringify(expenses));
	};
	import dateFormat, { masks } from 'dateformat';
	import { onMount } from 'svelte';

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
</script>

<h2>Expense Tracker</h2>

<form on:submit|preventDefault={NewExpense}>
	<label for="">Expense</label><input bind:value={name} type="text" /><label for="">Value</label
	><input bind:value={cost} type="text" /><label for="">Negative</label><input
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
<button
	on:click={() => {
		localStorage.clear();
		expenses = [];
	}}>Clear</button
>

<style>
	.negative {
		color: red;
	}
	.positive {
		color: green;
	}
	table {
		font-family: arial, sans-serif;
		border-collapse: collapse;
		width: 100%;
	}

	td,
	th {
		border: 1px solid #dddddd;
		text-align: left;
		padding: 8px;
	}

	tr:nth-child(even) {
		background-color: #dddddd;
	}
</style>
