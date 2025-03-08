<script lang="ts">
	import { cn } from '$lib/cn';

	let screenWidth = $state(0);
	let screenHeight = $state(0);

	let width = $derived(screenWidth * 1.5);
	let height = $derived(screenHeight * 1.5);

	let nbAlex = $derived(Math.round(height / 96));

	let {
		class: _class,
		beat,
		playing
	}: { class?: string; beat: number; playing: boolean } = $props();

	let heightPercentLol = $derived(Math.min(Math.max((beat - 16) / 16, 0), 1));

	// Define the Bubble type
	interface Bubble {
		id: string;
		size: string;
		left: string;
		animationDuration: string;
	}

	// Initialize the bubbles array
	let bubbles: Bubble[] = [];

	// Function to create a new bubble
	function createBubble(): void {
		const bubble: Bubble = {
			id: Math.random().toString(36).substr(2, 9),
			size: Math.random() * 20 + 10 + 'px',
			left: Math.random() * 100 + 'vw',
			animationDuration: Math.random() * 5 + 3 + 's'
		};
		bubbles = [...bubbles, bubble];

		// Remove the bubble after the animation ends
		setTimeout(
			() => {
				bubbles = bubbles.filter((b) => b.id !== bubble.id);
			},
			parseFloat(bubble.animationDuration) * 1000
		);
	}

	// Create bubbles at intervals
	setInterval(createBubble, 500);
</script>

<svelte:window bind:innerWidth={screenWidth} bind:innerHeight={screenHeight} />

<div
	class={cn('w-screen h-screen overflow-hidden relative transition-transform', _class)}
	style="transform:translateY({(1 - heightPercentLol) * 100}%)"
>
	<div class="bg-gradient-to-t from-orange-900 to-yellow-500 w-screen h-screen"></div>
	<div
		class="absolute overflow-hidden -top-80 -left-100 h-screen -rotate-25"
		style="width:{width}px; height:{height}px"
	>
		{#each Array(nbAlex) as _, index (index)}
			<div
				class={cn(
					'w-full h-24 bg-[url(/mariachu/ALEXENDER.png)] bg-[auto_96px] bg-repeat hover:scale-200 transition-all duration-500 opacity-20',
					index % 2 ? 'anim' : 'anim-inverted',
					!playing && '![animation-play-state:paused]'
				)}
			></div>
		{/each}
	</div>
</div>

<style>
	.bubble-container {
		position: relative;
		width: 100vw;
		height: 100vh;
		overflow: hidden;
		background-color: #007bff;
	}

	.bubble {
		position: absolute;
		bottom: -50px;
		background-color: rgba(255, 255, 255, 0.7);
		border-radius: 50%;
		animation: rise var(--animation-duration) ease-out forwards;
	}

	@keyframes rise {
		to {
			transform: translateY(-150vh);
			opacity: 0;
		}
	}

	:root {
		--animation-duration: 2000ms; /* Default animation duration */
	}

	.anim {
		animation: translateAnimation var(--animation-duration) infinite reverse;
	}

	.anim-inverted {
		animation: translateAnimation var(--animation-duration) infinite alternate-reverse;
	}

	.wave {
		display: block;
		position: absolute;
		top: 0;
		height: 40px;
		width: 100%;
		background: rgb(57, 27, 112);
		transform: scale(1, 1);
	}

	.wave:before {
		content: '';
		display: block;
		position: absolute;
		border-radius: 100%;
		width: 100%;
		height: 300px;
		background-color: white;
		right: -25%;
		top: 20px;
	}

	.wave:after {
		content: '';
		display: block;
		position: absolute;
		border-radius: 100%;
		width: 100%;
		height: 300px;
		background-color: white;
		left: -25%;
		top: -240px;
		clip-path: ellipse(100% 15% at -15% 100%);
	}

	@keyframes translateAnimation {
		0% {
			transform: translateX(0);
		}
		50% {
			transform: translateX(200px);
		}
		100% {
			transform: translateX(0);
		}
	}
</style>
