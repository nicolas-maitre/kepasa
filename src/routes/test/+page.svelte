<script lang="ts">
	import { cn } from '$lib/cn';

	let screenWidth = $state(0);
	let screenHeight = $state(0);

	let width = $derived(screenWidth * 1.5);
	let height = $derived(screenHeight * 1.5);

	let nbAlex = $derived(Math.round(height / 96));
</script>

<svelte:window bind:innerWidth={screenWidth} bind:innerHeight={screenHeight} />

<div class="w-screen h-screen overflow-hidden relative">
	<div class="bg-gradient-to-t from-orange-900 to-yellow-500 w-screen h-screen"></div>
	<div
		class="absolute overflow-hidden -top-80 -left-100 h-screen -rotate-25"
		style="width:{width}px; height:{height}px"
	>
		{#each Array(nbAlex) as _, index (index)}
			<div
				class={cn(
					'w-full h-24 bg-[url(/mariachu/ALEXENDER.png)] bg-[auto_96px] bg-repeat hover:scale-200 transition-all duration-500 opacity-20',
					index % 2 ? 'anim' : 'anim-inverted'
				)}
			></div>
		{/each}
	</div>
</div>

<style>
	:root {
		--animation-duration: 2000ms; /* Default animation duration */
	}

	.anim {
		animation: translateAnimation var(--animation-duration) infinite reverse;
	}

	.anim-inverted {
		animation: translateAnimation var(--animation-duration) infinite alternate-reverse;
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
