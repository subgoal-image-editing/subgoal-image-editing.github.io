<script>
	import Susie from './Susie.svelte';
	import { base } from '$app/paths';

	export let isOpen;

	const videoNames = [
		'move-the-wooden-bowl-to-the-top-of-the-table',
		'put-the-carrot-on-the-plate',
		'put-the-eggplant-in-the-pot',
		'put-the-eggplant-on-the-plate',
		'put-the-green-spoon-in-the-wooden-bowl',
		'put-the-orange-crayon-in-the-wooden-bowl',
		'put-the-toothpaste-in-the-wooden-bowl',
		'put-the-yellow-bell-pepper-in-the-ceramic-bowl',
		'put-the-yellow-bell-pepper-in-the-orange-pot'
	];
</script>

<div class="flex flex-col items-center mt-4 mb-4">
	<div class="w-full lg:w-11/12 flex flex-wrap justify-center mb-8">
		{#each videoNames as name}
			<div class="flex flex-col max-w-[150px] px-2 py-2">
				<div class="rounded-lg overflow-hidden">
					<video
						disableRemotePlayback
						muted
						webkit-playsinline
						playsinline
						loop
						autoplay
						src={isOpen ? `${base}/real/${name}.mp4` : ""}
					/>
				</div>
				<div class="text-center pt-1 leading-4 text-xs">
					&ldquo;{name.replaceAll('-', ' ')}&rdquo;
				</div>
			</div>
		{/each}
	</div>

	<table class="w-full lg:w-10/12 border-collapse text-center text-xs md:text-base">
		<thead>
			<tr class="border-t-2 border-black border-b-2">
				<th rowspan="2" />
				<th class="text-left" rowspan="2">Task</th>
				<th>LCBC</th>
				<th><a href="https://robot-moo.github.io/">MOO</a></th>
				<th><a href="https://universal-policy.github.io/unipi/">UniPi<span class="text-black"><sup>†</sup></span></a></th>
				<th><a href="https://robotics-transformer-x.github.io/">RT-2-X</a></th>
				<th><b><Susie /></b></th>
			</tr>
		</thead>
		<tbody>
			<!-- Scene A -->
			<tr>
				<td rowspan="4" class="scene-row border-b border-black">Scene A</td>
				<td>Eggplant on plate</td>
				<td>0.9</td>
				<td>0.4</td>
				<td>0.0</td>
				<td>0.3</td>
				<td><b>1.0</b></td>
			</tr>
			<tr>
				<td>Carrot on plate</td>
				<td>0.4</td>
				<td>0.3</td>
				<td>0.0</td>
				<td>0.6</td>
				<td><b>0.9</b></td>
			</tr>
			<tr>
				<td>Eggplant in pot</td>
				<td>0.6</td>
				<td><b>0.7</b></td>
				<td>0.0</td>
				<td>0.4</td>
				<td><b>0.7</b></td>
			</tr>
			<tr class="border-t border-black border-b">
				<td>Average</td>
				<td>0.63</td>
				<td>0.47</td>
				<td>0.0</td>
				<td>0.43</td>
				<td><b>0.87</b></td>
			</tr>
			<!-- Scene B -->
			<tr>
				<td rowspan="3" class="scene-row border-b border-black">Scene B</td>
				<td>Bell pepper in pot</td>
				<td>0.1</td>
				<td>0.0</td>
				<td>0.0</td>
				<td>0.0</td>
				<td><b>0.5</b></td>
			</tr>
			<tr>
				<td>Bell pepper in bowl</td>
				<td>0.3</td>
				<td>0.1</td>
				<td>0.1</td>
				<td>0.0</td>
				<td><b>0.5</b></td>
			</tr>
			<tr class="border-t border-black border-b">
				<td>Average</td>
				<td>0.20</td>
				<td>0.05</td>
				<td>0.05</td>
				<td>0.00</td>
				<td><b>0.50</b></td>
			</tr>
			<!-- Scene C -->
			<tr>
				<td rowspan="5" class="scene-row border-b-2 border-black">Scene C</td>
				<td>Toothpaste in bowl</td>
				<td>0.0</td>
				<td>0.0</td>
				<td>0.0</td>
				<td>0.5</td>
				<td><b>0.6</b></td>
			</tr>
			<tr>
				<td>Crayon in bowl</td>
				<td>0.0</td>
				<td>0.0</td>
				<td>0.0</td>
				<td>0.9</td>
				<td><b>1.0</b></td>
			</tr>
			<tr>
				<td>Spoon in bowl</td>
				<td>0.1</td>
				<td>0.3</td>
				<td>0.1</td>
				<td>0.7</td>
				<td><b>0.9</b></td>
			</tr>
			<tr>
				<td>Bowl to top</td>
				<td>0.6</td>
				<td>0.1</td>
				<td>0.1</td>
				<td>0.9</td>
				<td><b>1.0</b></td>
			</tr>
			<tr class="border-t border-black border-b-2">
				<td>Average</td>
				<td>0.18</td>
				<td>0.10</td>
				<td>0.05</td>
				<td>0.75</td>
				<td><b>0.88</b></td>
			</tr>
		</tbody>
	</table>

    <div class="mt-2 flex justify-center text-xs md:text-base">
        <div class="px-4"><sup>†</sup>Our implementation</div>
    </div>
</div>

<style>
	tr > td:first-child {
		text-align: left;
	}

	.scene-row + td {
		text-align: left;
	}

	th {
		font-weight: normal;
	}
</style>
