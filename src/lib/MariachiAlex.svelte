<script lang="ts">
	import { cn } from './cn';

	let {
		class: _class,
		beat,
		playing
	}: { class?: string; beat: number; playing: boolean } = $props();
</script>

<div
	class={cn(
		'relative size-52 *:absolute *:size-[inherit]',
		!playing && '*:![animation-play-state:paused]'
	)}
>
	<img src="/mariachi-alex/body.png" alt=":)" />
	<img src="/mariachi-alex/guitar.png" alt=":)" class="animate-guitar" />
	<img src="/mariachi-alex/hat.png" alt=":)" class="animate-hat" />
	<!-- </div> -->

	<img src="/mariachi-guitar/hand.png" alt=":)" class="animate-hand top-1/20" />
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
	@keyframes guitar-animation {
		from {
			transform: rotate(-2deg);
		}
		to {
			transform: rotate(-7deg);
		}
	}
	.animate-guitar {
		/* transform-origin: ; */
		animation: 500ms guitar-animation infinite alternate-reverse linear;
	}
	@keyframes hat-animation {
		from {
			transform: scaleY(1);
		}
		to {
			transform: scaleY(1.1);
		}
	}
	.animate-hat {
		/* transform-origin: ; */
		animation: 800ms hat-animation infinite alternate-reverse linear;
	}
</style>
