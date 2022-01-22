<script>

	let sliderVal = 1;
 
 let checkboxYes = false;
 	
 	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
	const progress = tweened(0, {
		duration: 400,
		easing: cubicOut
	});

	import { fade } from 'svelte/transition';
	let visibleFade = true;

	import { fly } from 'svelte/transition';
	let visibleFly = true;

	let visibleFadeFly = true;

	import { slide } from 'svelte/transition';
	let showItems = true;
	let i = 5;
	let items = ['one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine', 'ten'];
</script>

<main>
<!-- toc -->
	<a href="#slider">slider</a> | 
	<a href="#checkbox">toggle checkbox</a> |
	<a href="#tweening">tweening</a> | 
	<a href="#fade">fade</a> | 
	<a href="#fly">fly</a> | 
	<a href="#fly-inFade-out">fly-in/dafe-out</a> | 
	<a href="#local">local transition</a> | 

	<!-- slider -->
	<br /><br /><br /><br />
	<p><a id="slider">slider</a></p><hr>
	<label>
		<input type=number bind:value={sliderVal} min=0 max=10>
		<input type=range bind:value={sliderVal} min=0 max=10>
	</label>
	<p>{sliderVal}</p>
	
	<!-- checkbox -->
	<br /><br /><br /><br />
	<p><a id="checkbox">toggle checkbox</a></p><hr>
	<label>
		<input type=checkbox bind:checked={checkboxYes}>blah blah
	</label>
		{#if checkboxYes}
			<p>false</p>
		{:else}
			<p>true</p>
		{/if}
	<button disabled={!checkboxYes}>Subscribe</button>

	<!-- tweening -->
	<br /><br /><br /><br />
	<p><a id="tweening">tweening</a></p><hr>
	<progress value={$progress}></progress>
	<button on:click="{() => progress.set(0)}">0%</button>
	<button on:click="{() => progress.set(0.25)}">25%</button>
	<button on:click="{() => progress.set(0.5)}">50%</button>
	<button on:click="{() => progress.set(0.75)}">75%</button>
	<button on:click="{() => progress.set(1)}">100%</button>

	<!-- fade -->
	<br /><br /><br /><br />
	<p><a id="fade">fade</a></p><hr>
	<label>
		<input type="checkbox" bind:checked={visibleFade}>visible
	</label>
	{#if visibleFade}
		<p transition:fade>Fades in and out</p>
	{/if}

	<!-- fly -->
	<br /><br /><br /><br />
	<p><a id="fly">fly</a></p><hr>
	<label>
		<input type="checkbox" bind:checked={visibleFly}>visible</label>
	{#if visibleFly}
		<p transition:fly="{{ y: 200, duration: 2000 }}">Flies in and out</p>
	{/if}

	<!-- fly-in/fade-out -->
	<br /><br /><br /><br />
	<p><a id="fly-inFade-out">fly</a></p><hr>
	<label>
		<input type="checkbox" bind:checked={visibleFadeFly}>visible
	</label>
	{#if visibleFadeFly}
		<p in:fly="{{ y: 200, duration: 2000 }}" out:fade>Flies in, fades out</p>
	{/if}

	<!-- local transition -->
	<br /><br /><br /><br />
	<p><a id="local">local transition</a></p><hr>
	<label><input type="checkbox" bind:checked={showItems}>show list</label>
	<label><input type="range" bind:value={i} max=10></label>
	{#if showItems}
		{#each items.slice(0, i) as item}
			<div transition:slide|local>
				{item}
			</div>
		{/each}
	{/if}

	<!-- local transition -->
	<br /><br /><br /><br />
	<p><a id="local">local transition</a></p><hr>
</main>

<style>
	label { display: flex }
	input, p { margin: 6px }
	progress {
		display: block;
		width: 100%;
	}
	div {
		padding: 0.5em 0;
		border-top: 1px solid #eee;
	}
</style>