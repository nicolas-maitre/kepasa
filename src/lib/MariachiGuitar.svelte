<script lang="ts">
	import { cn } from './cn';

	let {
		class: _class,
		beat,
		playing
	}: { class?: string; beat: number; playing: boolean } = $props();
</script>

<div class="relative size-52 *:absolute *:size-[inherit]">
	<img src="/mariachi-guitar/body.png" alt=":)" />
	<img
		src="/mariachi-guitar/hand.png"
		alt=":)"
		class={cn('animate-hand', !playing && '![animation-play-state:paused]')}
	/>
</div>

<style>
	@keyframes hand-animation {
		from {
			transform: rotate(-25deg);
		}
		to {
			transform: rotate(25deg);
		}
	}
	.animate-hand {
		transform-origin: 20% 50%;
		animation: 200ms hand-animation infinite alternate-reverse linear;
	}
</style>
