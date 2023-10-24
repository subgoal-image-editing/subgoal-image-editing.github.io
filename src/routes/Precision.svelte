<script>
	import Collapsible from './Collapsible.svelte';
	import Susie from './Susie.svelte';
	import { base } from '$app/paths';

	const videoNames = [
		'open-the-drawer',
		'open-the-microwave',
		'put-the-coffee-creamer-in-the-drawer',
		'put-the-coffee-creamer-on-the-plate',
		'put-the-marker-on-the-towel',
		'put-the-yellow-bell-pepper-in-the-ceramic-bowl'
	];
</script>

<p class="mt-2">
	We were surprised to find that <Susie /> did not just help with zero-shot generalization, but also
	seemed to help significantly with low-level precision. To put this to the test, we evaluated an
	<b>Oracle GCBC</b> baseline, where we trained a goal-conditioned policy to reach any state in a
	trajectory and then provided that policy with <i>ground-truth</i> goal images at test time. Unlike <Susie
	/>, this method does not need to interpret the language instruction or otherwise do any semantic
	reasoning. It uses the exact same policy architecture and hyperparameters as the low-level policy
	in <Susie />, meaning any remaining advantage from <Susie /> must come from the way it breaks down
	the task hierarchically.
</p>

<p class="mt-2">
	Quantitatively, Oracle GCBC is one of the strongest baselines. However, it is still outperformed
	by <Susie /> on average, and fails to precisely manipulate objects in many scenarios where <Susie
	/> succeeds. For instance, <Susie /> is the only method that can consistently grasp the yellow bell
	pepper, which is light, smooth, and almost as wide as the gripper. In "put the marker on the towel,"
	observe how the low-level policy cannot grasp the marker until <Susie /> proposes a subgoal that clearly
	demonstrates the correct grasp height. In "put the coffee creamer on the plate," watch as both methods
	make the same mistake (early dropping); however, <Susie /> easily gets back on track thanks to subgoal
	guidance.
</p>

<div class="mt-2 ml-4">
	<Collapsible>
		<h3 slot="header" class="text-xl">Comparison Videos</h3>
		<div slot="body" class="mt-2 flex justify-center" let:isOpen>
			<div class="flex flex-col items-center mb-4">
				<div class="w-full lg:w-11/12 flex flex-wrap justify-center">
					{#each videoNames as name}
						<div class="flex flex-col max-w-[300px] px-2 py-2">
							<div class="flex justify-center">
								<div class="flex flex-col">
									<div class="text-center pb-1 text-sm">
										<Susie />
									</div>
									<div class="rounded-lg overflow-hidden">
										<video
											disableRemotePlayback
											muted
											webkit-playsinline
											playsinline
											loop
											autoplay
											src={isOpen ? `${base}/comparison/ours/${name}.mp4` : ''}
										/>
									</div>
								</div>
								<div class="flex flex-col">
									<div class="text-center pb-1 text-sm">GCBC</div>
									<div class="rounded-lg overflow-hidden">
										<video
											disableRemotePlayback
											muted
											webkit-playsinline
											playsinline
											loop
											autoplay
											src={isOpen ? `${base}/comparison/gcbc/${name}.mp4` : ''}
										/>
									</div>
								</div>
							</div>
							<div class="text-center pt-1 leading-4 text-xs">
								&ldquo;{name.replaceAll('-', ' ')}&rdquo;
							</div>
						</div>
					{/each}
				</div>
			</div>
		</div></Collapsible
	>
	<div class="mt-2" />
	<Collapsible>
		<h3 slot="header" class="text-xl">Quantitative Results</h3>
		<div slot="body" class="mt-2 flex justify-center">
			<table class="w-full lg:w-10/12 border-collapse text-center text-xs md:text-base mt-1">
				<thead>
					<tr class="border-t-2 border-black border-b-2">
						<th rowspan="2" />
						<th class="text-left" rowspan="2">Task</th>
						<th>Oracle GCBC</th>
						<th><b><Susie /></b></th>
					</tr>
				</thead>
				<tbody>
					<!-- Scene A -->
					<tr>
						<td rowspan="4" class="scene-row border-b border-black">Scene A</td>
						<td>Eggplant on plate</td>
						<td>0.7</td>
						<td><b>1.0</b></td>
					</tr>
					<tr>
						<td>Carrot on plate</td>
						<td>0.8</td>
						<td><b>0.9</b></td>
					</tr>
					<tr>
						<td>Eggplant in pot</td>
						<td><b>1.0</b></td>
						<td>0.7</td>
					</tr>
					<tr class="border-t border-black border-b">
						<td>Average</td>
						<td>0.83</td>
						<td><b>0.87</b></td>
					</tr>
					<!-- Scene B -->
					<tr>
						<td rowspan="3" class="scene-row border-b border-black">Scene B</td>
						<td>Bell pepper in pot</td>
						<td>0.1</td>
						<td><b>0.5</b></td>
					</tr>
					<tr>
						<td>Bell pepper in bowl</td>
						<td>0.0</td>
						<td><b>0.5</b></td>
					</tr>
					<tr class="border-t border-black border-b">
						<td>Average</td>
						<td>0.05</td>
						<td><b>0.50</b></td>
					</tr>
					<!-- Scene C -->
					<tr>
						<td rowspan="5" class="scene-row border-b-2 border-black">Scene C</td>
						<td>Toothpaste in bowl</td>
						<td><b>0.7</b></td>
						<td>0.6</td>
					</tr>
					<tr>
						<td>Crayon in bowl</td>
						<td><b>1.0</b></td>
						<td><b>1.0</b></td>
					</tr>
					<tr>
						<td>Spoon in bowl</td>
						<td>0.8</td>
						<td><b>0.9</b></td>
					</tr>
					<tr>
						<td>Bowl to top</td>
						<td>0.6</td>
						<td><b>1.0</b></td>
					</tr>
					<tr class="border-t border-black border-b-2">
						<td>Average</td>
						<td>0.78</td>
						<td><b>0.88</b></td>
					</tr>
					<!-- CALVIN -->
					<tr>
						<td rowspan="5" class="scene-row border-b-2 border-black">CALVIN</td>
						<td>Move slider right/left</td>
						<td>0.52</td>
						<td><b>0.86</b></td>
					</tr>
					<tr>
						<td>Turn on/off light bulb</td>
						<td>0.74</td>
						<td><b>0.96</b></td>
					</tr>
					<tr>
						<td>Open/close drawer</td>
						<td><b>1.00</b></td>
						<td>0.98</td>
					</tr>
					<tr>
						<td>Turn on/off LED</td>
						<td>0.36</td>
						<td><b>1.00</b></td>
					</tr>
					<tr class="border-t border-black border-b-2">
						<td>Average</td>
						<td>0.66</td>
						<td><b>0.95</b></td>
					</tr>
				</tbody>
			</table>
		</div>
	</Collapsible>
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
