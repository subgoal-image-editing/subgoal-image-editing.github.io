<script>
	import Collapsible from './Collapsible.svelte';
	import Susie from './Susie.svelte';
	import { base } from '$app/paths';
</script>

<p class="mt-2">
	Since the image-editing model in <Susie /> does not require robot actions, it can leverage broad video
	for even greater zero-shot generalization. In addition to the robot demonstrations in
	<a href="https://rail-berkeley.github.io/bridgedata/">BridgeData</a>, we also trained <Susie /> on
	the
	<a href="https://developer.qualcomm.com/software/ai-datasets/something-something"
		>Something-Something</a
	>
	dataset, which contains 220,847 labeled video clips of humans manipulating various objects. Here, we
	present an ablation showing that the video data does indeed help, especially in the zero-shot setting.
	We hope that future work will explore scaling up <Susie /> to even larger and broader video datasets.
</p>

<div class="mt-2 ml-4">
	<Collapsible>
		<h3 slot="header" class="text-xl">Qualtitative Examples</h3>
		<div slot="body" class="flex flex-col items-center mt-8 mb-4 w-full">
			<div class="w-full lg:w-10/12">
				<img src="{base}/model_comparison_v2.svg" class="w-full" alt="teaser" />
			</div>
			<p class="italic mt-4">
				A comparison between 3 subgoal generation models: one trained on both robot and video data
				(Bridge + Smthn-Smthn), the primary <Susie /> model; one trained on robot data only (Bridge Only);
				and one trained without InstructPix2Pix initialization (From Scratch). The top half (In Distribution)
				comes from the BridgeData V2 validation set, while the bottom half (Out of Distribution) comes
				from our evaluation Scenes B and C, which are unseen in BridgeData V2.
			</p>
		</div>
	</Collapsible>
	<div class="mt-2" />
	<Collapsible>
		<h3 slot="header" class="text-xl">Quantitative Results</h3>
		<div slot="body" class="mt-2 flex justify-center">
			<table class="w-full lg:w-10/12 border-collapse text-center text-xs md:text-base mt-1">
				<thead>
					<tr class="border-t-2 border-black border-b-2">
						<th rowspan="2" />
						<th class="text-left" rowspan="2">Task</th>
						<th>BridgeData Only</th>
						<th>BridgeData + Something-Something</th>
					</tr>
				</thead>
				<tbody>
					<!-- Scene B -->
					<tr>
						<td rowspan="3" class="scene-row border-b border-black">Scene B</td>
						<td>Bell pepper in pot</td>
						<td>0.2</td>
						<td><b>0.5</b></td>
					</tr>
					<tr>
						<td>Bell pepper in bowl</td>
						<td>0.4</td>
						<td><b>0.5</b></td>
					</tr>
					<tr class="border-t border-black border-b">
						<td>Average</td>
						<td>0.30</td>
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
						<td><b>0.9</b></td>
						<td><b>1.0</b></td>
					</tr>
					<tr>
						<td>Spoon in bowl</td>
						<td><b>0.9</b></td>
						<td><b>0.9</b></td>
					</tr>
					<tr>
						<td>Bowl to top</td>
						<td>0.7</td>
						<td><b>1.0</b></td>
					</tr>
					<tr class="border-t border-black border-b-2">
						<td>Average</td>
						<td>0.80</td>
						<td><b>0.88</b></td>
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
