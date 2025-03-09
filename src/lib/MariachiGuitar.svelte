<script lang="ts">
	import { cn } from './cn';

	let {
		class: _class,
		beat,
		playing
	}: { class?: string; beat: number; playing: boolean } = $props();

	let jsp = $derived(beat - 1);
	let spinStep: 'fw' | 'bw' | 'nm' = $derived(
		playing && beat > 0 ? (+(jsp % 2 === Math.floor(jsp / 16) % 2) ? 'fw' : 'bw') : 'nm'
	);
</script>

<div
	class={cn(
		'relative size-75 *:absolute *:size-[inherit]',
		'transition-transform duration-200',
		spinStep === 'fw' && 'rotate-12',
		spinStep === 'bw' && '-rotate-12',
		spinStep === 'nm' && 'rotate-0'
	)}
>
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
