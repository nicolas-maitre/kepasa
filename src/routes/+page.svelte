<script lang="ts">
	import { PauseCircleIcon, PlayCircleIcon } from 'lucide-svelte';
	import KepaLogo from './KepaLogo.svelte';
	import { scale, fly, fade } from 'svelte/transition';
	import Background from './Background.svelte';
	import MariachiGuitar from '$lib/MariachiGuitar.svelte';
	import MariachiAlex from '$lib/MariachiAlex.svelte';
	let time = $state(0);
	let readyState = $state<number>();
	let paused = $state(true);
	let playing = $derived(!paused);
	let player = $state<HTMLAudioElement>();

	const startOffset = 6.6;
	// const bpm = 132;
	const bpm = 135;
	let beat = $derived(Math.max(Math.ceil(((time - startOffset) * bpm) / 60), 0));
	// let beat = $state(0);

	let isKepasaVisible = $derived(time > 1.8 && time < 6);
	let isQuestionVisible = $derived(time > 1.8 && time < 3);

	let showGuitarMariachis1 = $derived(beat > 32);
	let guitarMariachisProgress1 = $derived(Math.min(Math.max((beat - 32) / 8, 0), 1));
	let showGuitarMariachis2 = $derived(beat > 32 + 8);
	let guitarMariachisProgress2 = $derived(Math.min(Math.max((beat - (32 + 8)) / 8, 0), 1));

	let showAlexMariachis1 = $derived(beat > 32 + 16);
	let alexMariachisProgress1 = $derived(Math.min(Math.max((beat - (32 + 16)) / 8, 0), 1));
	let showAlexMariachis2 = $derived(beat > 32 + 16 + 8);
	let alexMariachisProgress2 = $derived(Math.min(Math.max((beat - (32 + 16 + 8)) / 8, 0), 1));
</script>

<main class="relative">
	<div class="h-screen w-screen absolute overflow-hidden top-0">
		<Background class="absolute z-0" {beat} {playing} />
	</div>
	<div
		class="absolute flex flex-col justify-center items-center h-screen w-screen overflow-hidden z-10 pointer-events-none"
	>
		<div class="flex items-center font-extrabold text-[5rem] text-primary gap-2">
			{#if isKepasaVisible}
				<!-- only to keep it centered loul -->
				<p in:scale out:scale={{ start: 2 }} class="invisible">sa</p>
			{/if}
			{#if isQuestionVisible}
				<p in:fly={{ y: '100%' }} out:scale={{ start: 2 }}>¿</p>
			{/if}
			<KepaLogo {beat} playing={!paused} class="size-52 mt-3" />
			{#if isKepasaVisible}
				<p in:scale out:scale={{ start: 2 }}>sa</p>
			{/if}
			{#if isQuestionVisible}
				<p in:fly={{ y: '-100%' }} out:scale={{ start: 2 }}>?</p>
			{/if}
		</div>
		<!-- <MariachiAlex />
		<MariachiGuitar /> -->
		<button
			onclick={() => (paused ? player?.play() : player?.pause())}
			disabled={readyState !== 4}
			class="disabled:opacity-50 cursor-pointer *:size-16 *:stroke-primary pointer-events-auto"
		>
			{#if paused}
				<PlayCircleIcon />
			{:else}
				<PauseCircleIcon />
			{/if}
		</button>
		<!-- controls -->
		<audio
			bind:currentTime={time}
			bind:paused
			bind:readyState
			bind:this={player}
			src="/soundtrack.mp3"
			autoplay={false}
			class="pointer-events-auto"
		></audio>
		<!-- {time}
		<br />
		{beat} -->
		<div class="*:flex *:*:-mx-8 *:absolute *:bottom-0 w-screen overflow-hidden">
			<!-- mariachis guitar -->
			{#if showGuitarMariachis1}
				<div
					class="transition-[right]"
					style="right:{(1 - guitarMariachisProgress1) * 60 + 50}%"
					out:fade
				>
					<MariachiGuitar {playing} {beat} />
					<MariachiGuitar {playing} {beat} />
					<MariachiGuitar {playing} {beat} />
					<MariachiGuitar {playing} {beat} />
					<MariachiGuitar {playing} {beat} />
				</div>
			{/if}
			{#if showGuitarMariachis2}
				<div
					class="transition-[left]"
					style="left:{(1 - guitarMariachisProgress2) * 60 + 50}%"
					out:fade
				>
					<MariachiGuitar {playing} {beat} />
					<MariachiGuitar {playing} {beat} />
					<MariachiGuitar {playing} {beat} />
					<MariachiGuitar {playing} {beat} />
					<MariachiGuitar {playing} {beat} />
				</div>
			{/if}
		</div>
		<div class="*:flex *:*:-mx-8 *:absolute *:top-0 w-screen overflow-hidden">
			{#if showAlexMariachis1}
				<!-- mariachis guitar -->
				<div
					class="transition-[right]"
					style="right:{(1 - alexMariachisProgress1) * 60 + 50}%"
					out:fade
				>
					<MariachiAlex {playing} {beat} />
					<MariachiAlex {playing} {beat} />
					<MariachiAlex {playing} {beat} />
					<MariachiAlex {playing} {beat} />
					<MariachiAlex {playing} {beat} />
				</div>
			{/if}
			{#if showAlexMariachis2}
				<div
					class="transition-[left]"
					style="left:{(1 - alexMariachisProgress2) * 60 + 50}%"
					out:fade
				>
					<MariachiAlex {playing} {beat} />
					<MariachiAlex {playing} {beat} />
					<MariachiAlex {playing} {beat} />
					<MariachiAlex {playing} {beat} />
					<MariachiAlex {playing} {beat} />
				</div>
			{/if}
		</div>
	</div>
</main>
