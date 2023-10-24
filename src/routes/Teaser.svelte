<script>
	import Carousel from 'svelte-carousel';
	import MediaQuery from './MediaQuery.svelte';
	import { browser } from '$app/environment';
	import { base } from '$app/paths';

	let carousel;

	const videoNames = [
		'put-the-yellow-block-in-the-drawer',
		'move-the-wooden-bowl-to-the-top-of-the-table',
		'put-the-yellow-bell-pepper-in-the-ceramic-bowl',
		'open-the-drawer',
		'open-the-microwave',
		'put-the-coffee-creamer-on-the-plate',
		'close-the-drawer',
		'put-the-eggplant-in-the-pot',
		'put-the-toothpaste-in-the-wooden-bowl',
		'put-the-yellow-bell-pepper-in-the-orange-pot'
	];

	const videoData = videoNames.map((name) => ({
		src: `teaser/${name}.mp4`,
		text: name.replaceAll('-', ' ')
	}));

	const videos = [];
	const paused = Array(videoData.length).fill(true);

	let isWide;
	$: offset = isWide ? 1 : 0;

	function handleChange(event) {
		const curr = (event.detail + offset + videoData.length) % videoData.length;
		for (let i = 0; i < videoData.length; i++) {
			if (i !== curr) {
				paused[i] = true;
			}
		}
		paused[curr] = false;
		// videos.forEach((video, i) => {
		// 	if (!video.paused && !video.ended && i !== curr) {
		// 		video.pause();
		// 	}
		// });
		// Array.from(document.getElementsByClassName('sc-carousel-button')).forEach((button) => {
		// 	button.disabled = true;
		// });

		// const reEnable = () => {
		// 	Array.from(document.getElementsByClassName('sc-carousel-button')).forEach((button) => {
		// 		button.disabled = false;
		// 	});
		// };
		// videos[curr].play().then(reEnable, reEnable);
		// console.log("playing", curr);
	}
</script>

{#if browser}
	<MediaQuery query="(min-width: 768px)" bind:matches={isWide} />
	<div class="w-full" class:wide={isWide} id="container">
		<Carousel
			bind:this={carousel}
			particlesToShow={isWide ? 3 : 1}
			swiping={false}
			on:pageChange={handleChange}
		>
			{#each videoData as video, i}
				<div class="px-2 flex flex-col">
					<div class="rounded-lg overflow-hidden">
						<video
							disableRemotePlayback
							muted
							webkit-playsinline
							playsinline
							bind:this={videos[i]}
							bind:paused={paused[i]}
							on:ended={() => carousel.goToNext()}
							autoplay={i === 0}
							src="{base}/{video.src}"
						/>
					</div>
					<div class="text-center pt-1 leading-5">
						&ldquo;{video.text}&rdquo;
					</div>
				</div>
			{/each}
		</Carousel>
		{#if isWide}
			<div id="mask" />
		{/if}
	</div>
{/if}

<style>
	#container {
		position: relative;
	}
	#mask {
		position: absolute;
		right: 0;
		bottom: 0;
		left: 0;
		top: 0;
		background: linear-gradient(to right, white 15%, transparent 30%, transparent 70%, white 85%);
		z-index: 0;
	}

	:global(.sc-carousel__arrow-container) {
		z-index: 100;
	}

	:global(.wide .sc-carousel__arrow-container):first-child {
		transform: translateX(200%);
	}

	:global(.wide .sc-carousel__arrow-container):last-child {
		transform: translateX(-200%);
	}
</style>
