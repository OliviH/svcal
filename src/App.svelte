<script>
	import { onMount } from 'svelte'
	import Calendar from './components/Calendar.svelte'
	
	export let name;

	let cal = {},
		bindCal = null

	cal.today = new Date().toISOString()

	$:{
		if(cal) console.log('cal change', cal)
	}
	onMount(() => {
		bindCal.selectmonth(cal.today)
	})

</script>

<main>
	<h1>{name}</h1>
	<hr>
</main>
<Calendar
	cal={cal}
	bind:this={bindCal}
/>