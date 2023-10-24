<script>
	export let video;
</script>

<div class="rounded-lg overflow-hidden">
	<video
		disableRemotePlayback
		muted
		webkit-playsinline
		playsinline
		loop
		bind:this={video}
		{...$$props}
	/>
</div>
