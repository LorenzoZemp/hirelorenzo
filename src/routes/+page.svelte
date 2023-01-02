<script>
	// Libraries
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';

	// Styles and Icons
	import '@picocss/pico';
	import 'iconify-icon';

	let audio;
	let isPlaying = false;
	let isMuted = false;

	const strings = ['Reasons you should hire Lorenzo', "1. He's really cool", '2. Just do it'];

	let index = 0;
	let isVisible = true;

	function nextBtnClick() {
		//So that the audio is played after the first click
		if (!isPlaying) {
			audio.volume = 0.5;
			audio.play();
			isPlaying = true;
		}

		if (index === strings.length - 1) {
			isVisible = false;
			showScroller = true;
			return;
		}
		isVisible = false;
		setTimeout(() => {
			index++;
			isVisible = true;
		}, 500);
	}

	function muteBtnClick() {
		if (!isMuted) {
			audio.volume = 0;
			isMuted = true;
		} else {
			audio.volume = 0.5;
			isMuted = false;
		}
	}
</script>

<main class="container">
	{#if isVisible}
		<h1 transition:fade>{strings[index]}</h1>
	{/if}
	<button on:click={nextBtnClick}
		><iconify-icon icon="material-symbols:chevron-right-rounded" /></button
	>
	<audio
		src="https://docs.google.com/uc?export=download&id=16-DQKc10YF5aBWnaQ8i09TGyQaeD2OLx"
		bind:this={audio}
	/>
	<button on:click={muteBtnClick}>Mute</button>
</main>
