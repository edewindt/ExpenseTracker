<script>
	import { v4 as uuidv4 } from 'uuid';
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
			id: uuidv4(),
			name,
			cost,
			negative,
			time: dateFormat(new Date(), 'dddd, mmmm dS, yyyy, h:MM:ss TT'),
			clicked: false
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

	const updateRes = () => {
		localStorage.clear;
		localStorage.setItem('expenses', JSON.stringify(expenses));
	};
	const del = (id) => {
		const res = expenses.filter((o) => o.id != id);
		expenses = res;
		updateRes();
	};

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
	<tr><th>Expense</th><th>Value</th><th>Time</th><th>Edit</th></tr>
	{#each expenses as e (e.id)}
		{#if e.clicked}<tr
				><td><input type="text" bind:value={e.name} /></td><td
					><input type="text" bind:value={e.cost} /></td
				><td>{e.time}</td><td
					><button
						on:click={() => {
							e.clicked = !e.clicked;
							updateRes();
						}}>save</button
					></td
				></tr
			>{:else}<tr
				><td>{e.name}</td><td class:negative={e.negative} class:positive={!e.negative}
					>{#if e.negative}- ${e.cost}{:else}+ ${e.cost}{/if}</td
				><td>{e.time}</td><td
					><button
						on:click={() => {
							e.clicked = !e.clicked;
						}}>edit</button
					>
					<button
						on:click={() => {
							del(e.id);
						}}>delete</button
					></td
				></tr
			>{/if}
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
		background-color: #ffefef;
	}
	.positive {
		color: green;
		background-color: rgb(193, 255, 194);
	}
	tr:nth-child(even) .negative {
		background-color: #ffcece;
	}
	tr:nth-child(even) .positive {
		background-color: rgb(222, 255, 223);
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
	td input {
		max-width: 100%;
	}
</style>
