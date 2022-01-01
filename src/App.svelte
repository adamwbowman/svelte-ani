<script>

	// slider
	let sliderVal = 1;
 
	// toggle checkbox
	let checkboxYes = false;

	// tweening
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
	const progress = tweened(0, {
		duration: 400,
		easing: cubicOut
	});

	// fade
	import { fade } from 'svelte/transition';
	let visibleFade = true;

	// fly
	import { fly } from 'svelte/transition';
	let visibleFly = true;

	// fly-in/fade-out
	let visibleFadeFly = true;

	// local transition
	import { slide } from 'svelte/transition';
	let showItems = true;
	let i = 5;
	let items = 
		['one', 'two', 'three', 'four', 'five', 
		'six', 'seven', 'eight', 'nine', 'ten'];

	// key blocks
	let keyNumber = 0;

	// use directice
	import { clickOutside } from "./click_outside.js";
	let showModal = true;

	// class directive
	let current = 'foo';

	// shorthand directive
	let big = false;

	// working
	let tests = [
		{id: "23532354", name: "asdfasdf"},
		{id: "86456764", name: "dfgbdfgb"},
		{id: "34563456", name: "yurjrjuy"},
		{id: "97573576", name: "fghkfghk"},
		{id: "85678886", name: "yuikyuku"}
	]
</script>

<main>
<!-- working -->
<button type="button" on:click="{() => tests = [...tests.slice(0, tests.length -1)]}">remove item</button>
<button type="button" on:click="{() => tests = [...tests, tests.length + 1]}">add item</button>

{#each tests as test}
	<div in:slide out:fade>{test.id}:{test.name}
	<button on:click="{() => tests = tests.filter(el => el.id != test.id)}">x</button>
	</div>
{/each}

<br /><br /><br /><br /><br /><br /><br />

<!-- toc -->
	<a href="#slider">slider</a> | 
	<a href="#checkbox">toggle checkbox</a> |
	<a href="#tweening">tweening</a> | 
	<a href="#fade">fade</a> | 
	<a href="#fly">fly</a> | 
	<a href="#fly-inFade-out">fly-in/dafe-out</a> | 
	<a href="#local">local transition</a> | 
	<a href="#key">key blocks</a> | 
	<a href="#use">use directive</a> | 
	<a href="#class">class directive</a> | 
	<a href="#short">shorthand directive</a> | 

	<!-- slider -->
	<br /><br /><br /><br /><br />
	<p><a id="slider">slider</a></p><hr>
	<label>
		<input type=number bind:value={sliderVal} min=0 max=10>
		<input type=range bind:value={sliderVal} min=0 max=10>
	</label>
	<p>{sliderVal}</p>

	<!-- checkbox -->
	<br /><br /><br /><br /><br />
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
	<br /><br /><br /><br /><br />
	<p><a id="tweening">tweening</a></p><hr>
	<progress value={$progress}></progress>
	<button on:click="{() => progress.set(0)}">0%</button>
	<button on:click="{() => progress.set(0.25)}">25%</button>
	<button on:click="{() => progress.set(0.5)}">50%</button>
	<button on:click="{() => progress.set(0.75)}">75%</button>
	<button on:click="{() => progress.set(1)}">100%</button>

	<!-- fade -->
	<br /><br /><br /><br /><br />
	<p><a id="fade">fade</a></p><hr>
	<label>
		<input type="checkbox" bind:checked={visibleFade}>visible
	</label>
	{#if visibleFade}
		<p transition:fade>Fades in and out</p>
	{/if}

	<!-- fly -->
	<br /><br /><br /><br /><br />
	<p><a id="fly">fly</a></p><hr>
	<label>
		<input type="checkbox" bind:checked={visibleFly}>visible</label>
	{#if visibleFly}
		<p transition:fly="{{ y: 200, duration: 2000 }}">Flies in and out</p>
	{/if}

	<!-- fly-in/fade-out -->
	<br /><br /><br /><br /><br />
	<p><a id="fly-inFade-out">fly-in/fade-out</a></p><hr>
	<label>
		<input type="checkbox" bind:checked={visibleFadeFly}>visible
	</label>
	{#if visibleFadeFly}
		<p in:fly="{{ y: 200, duration: 2000 }}" out:fade>Flies in, fades out</p>
	{/if}

	<!-- local transition -->
	<br /><br /><br /><br /><br />
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

	<!-- key block -->
	<br /><br /><br /><br /><br />
	<p><a id="key">key block</a></p><hr>
	<div>The number is:
		{#key keyNumber}
			<span style="display: inline-block" 
				in:fly={{ y: -20 }}>
				{keyNumber}
			</span>
		{/key}
	</div><br />
	<button
		on:click={() => {
			keyNumber += 1;
		}}>
		Increment
	</button>

	<!-- use directive -->
	<br /><br /><br /><br /><br />
	<p><a id="use">use directive</a></p><hr>
	<button 
		on:click={() => (showModal = true)}>
		Show Modal
	</button>
	{#if showModal}
		<div class="usebox" 
			use:clickOutside 
			on:outclick={() => (showModal = false)}>
			Click outside me!
		</div>
	{/if}
	
	<!-- class directive -->
	<br /><br /><br /><br /><br />
	<p><a id="class">class directive</a></p><hr>
	<button
		class:selected="{current === 'foo'}"
		on:click="{() => current = 'foo'}"
		>foo</button>
	<button
		class:selected="{current === 'bar'}"
		on:click="{() => current = 'bar'}"
	>bar</button>
	<button
		class:selected="{current === 'baz'}"
		on:click="{() => current = 'baz'}"
	>baz</button>

	<!-- shorthand directive -->
	<br /><br /><br /><br /><br />
	<p><a id="short">shorthand directive</a></p><hr>
	<label>
		<input type=checkbox bind:checked={big}>
		big
	</label>
	<div class:big>
		some {big ? 'big' : 'small'} text
	</div>
	





	<br /><br /><br /><br /><br /><br /><br />
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
	.usebox {
		--width: 100px;
		--height: 100px;
		position: relative;
		width: var(--width);
		height: var(--height);
		left: calc(50% - var(--width) / 2);
		top: calc(50% - var(--height) / 2);
		border-radius: 4px;
		background-color: #ff3e00;
		color: #fff;
		text-align: center;
		font-weight: bold;
	}
	button {
		display: block;
	}
	.selected {
		background-color: #ff3e00;
		color: white;
	}
	.big {
		font-size: 4em;
	}
</style>