<script lang="ts">
	import anime from 'animejs';
	import { onMount } from 'svelte';

	onMount(() => {
		const dotsFragment = document.createDocumentFragment();
		const grid = [10, 10];
		var numberOfElements = grid[0] * grid[1];

		for (let i = 0; i < numberOfElements; i++) {
			const dot = document.createElement('div');
			dot.classList.add('dot');
			dotsFragment.appendChild(dot);
		}

		const wrapper = document.querySelector('.dots-wrapper');
		wrapper!.appendChild(dotsFragment);
		// create a timeline
		const tl = anime.timeline({
			// loop and reverse the animation
			loop: true,
			direction: 'alternate'
		});

		// add animations to the timeline
		tl.add({
			targets: '.dot',
			scale: [0.1, 1],
			// stagger from center
			delay: anime.stagger(25, { from: 'center' }),
			duration: 250,
			easing: 'easeInOutQuad'
		})
			// move up
			.add({
				targets: '.dot',
				translateY: -100,
				delay: anime.stagger(15, { from: 'center' }),
				duration: 500,
				easing: 'easeInOutQuad'
			})
			// move down
			.add({
				targets: '.dot',
				translateY: 0,
				delay: anime.stagger(10, { from: 'first' }),
				duration: 350,
				easing: 'easeInOutQuad'
			});
	});
</script>

<div class="container h-full w-full max-w-max m-auto">
	<div class="flex justify-center items-center h-full">
		<div class="stage">
			<div
				class="wrapper dots-wrapper flex flex-wrap align-content-center align-items-center flex-row justify-center"
			/>
		</div>
	</div>
</div>

<style lang="postcss">
	.stage {
		width: 100%;
		margin: 0 auto;
	}

	:global(.dot) {
		width: 10px;
		height: 10px;
		background: #009dff;
		border-radius: 50%;
		margin: 0px;
	}
</style>
