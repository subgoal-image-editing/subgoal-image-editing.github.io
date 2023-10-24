<script>
	import Susie from './Susie.svelte';
	import { base } from '$app/paths';

    export let isOpen;

	const videoNames = [
		'go-push-the-blue-block-right',
		'lift-the-blue-block-from-the-sliding-cabinet',
		'lift-the-red-block-from-the-sliding-cabinet',
		'pull-the-handle-to-open-the-drawer',
		'take-the-blue-block-and-rotate-it-to-the-left'
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
						src={isOpen ? `${base}/calvin/${name}.mp4` : ""}
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
			<tr class="border-b border-t-2 border-black">
				<th class="w-8" rowspan="2" />
				<th class="" colspan="5">Success Rate for No. of Instructions in a Row</th>
				<th class="w-24" rowspan="2">Avg. No. of Instructions Completed</th>
			</tr>
			<tr class="border-b-2 border-black">
				<th class="w-8">1</th>
				<th class="w-8">2</th>
				<th class="w-8">3</th>
				<th class="w-8">4</th>
				<th class="w-8">5</th>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td><a href="http://hulc.cs.uni-freiburg.de/">HULC</a></td>
				<td>0.43</td>
				<td>0.14</td>
				<td>0.04</td>
				<td>0.01</td>
				<td>0.00</td>
				<td>0.62</td>
			</tr>
			<tr>
				<td><a href="https://language-play.github.io/">MCIL</a></td>
				<td>0.20</td>
				<td>0.00</td>
				<td>0.00</td>
				<td>0.00</td>
				<td>0.00</td>
				<td>0.20</td>
			</tr>
			<tr>
				<td><a href="https://geyuying.github.io/PAFF/">MdetrLC</a></td>
				<td>0.69</td>
				<td>0.38</td>
				<td>0.20</td>
				<td>0.07</td>
				<td>0.04</td>
				<td>1.38</td>
			</tr>
			<tr>
				<td><a href="https://geyuying.github.io/PAFF/">AugLC</a></td>
				<td>0.69</td>
				<td>0.43</td>
				<td>0.22</td>
				<td>0.09</td>
				<td>0.05</td>
				<td>1.43</td>
			</tr>
			<tr>
				<td>LCBC</td>
				<td>0.67</td>
				<td>0.31</td>
				<td>0.17</td>
				<td>0.10</td>
				<td>0.06</td>
				<td>1.31</td>
			</tr>
			<tr>
				<td
					><a href="https://universal-policy.github.io/unipi/">UniPi<span class="text-black"><sup>*</sup></span></a>
					</td
				>
				<td>0.08</td>
				<td>0.04</td>
				<td>0.00</td>
				<td>0.00</td>
				<td>0.00</td>
				<td>0.12</td>
			</tr>
			<tr>
				<td><a href="https://universal-policy.github.io/unipi/">UniPi<span class="text-black"><sup>†</sup></span></a></td>
				<td>0.56</td>
				<td>0.16</td>
				<td>0.08</td>
				<td>0.08</td>
				<td>0.04</td>
				<td>0.92</td>
			</tr>
			<tr class="border-b-2 border-black">
				<td><b><Susie /></b></td>
				<td><b>0.87</b></td>
				<td><b>0.69</b></td>
				<td><b>0.49</b></td>
				<td><b>0.38</b></td>
				<td><b>0.26</b></td>
				<td><b>2.69</b></td>
			</tr>
		</tbody>
	</table>

    <div class="mt-2 flex justify-center text-xs md:text-base">
        <div class="px-4"><sup>*</sup><a href="https://hierarchical-planning-foundation-model.github.io/">HiP</a> implementation</div>
        <div class="px-4"><sup>†</sup>Our implementation</div>
    </div>
</div>

<style>
	tr > td:first-child {
		text-align: left;
	}

	th {
		font-weight: normal;
	}
</style>
