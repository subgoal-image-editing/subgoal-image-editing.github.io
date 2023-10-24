<script>
	import Susie from './Susie.svelte';
	import Teaser from './Teaser.svelte';
	import { base } from '$app/paths';
	import Collapsible from './Collapsible.svelte';
	import CalvinTable from './CalvinTable.svelte';
	import RealTable from './RealTable.svelte';
	import Precision from './Precision.svelte';
	import VideoData from './VideoData.svelte';
</script>

<div class="flex w-full justify-center mb-96">
	<div class="max-w-4xl w-full px-4 pt-12">
		<h1 class="font-bold text-4xl text-center mb-8">
			<Susie />: Subgoal Synthesis via Image Editing
		</h1>

		<!-- teaser -->
		<Teaser />

		<!-- intro -->
		<p class="mt-4">
			<Susie /> makes generalizable robotic manipulation as easy as finetuning an open-source image-editing
			model, such as
			<a href="https://www.timothybrooks.com/instruct-pix2pix">InstructPix2Pix</a>. Given an image
			and a language command, <Susie /> executes the command by "editing" the image into a meaningful
			subgoal and then achieving that subgoal using a low-level goal-reaching policy. Much like a person
			first constructs a high-level plan to complete a task before deferring to muscle memory for the
			low-level control,
			<Susie /> first leverages a simple image-generative model for visuo-semantic reasoning before deferring
			to a low-level policy to determine precise motor actuations.
		</p>
		<p class="mt-4">
			We find that this recipe enables significantly higher generalization and precision than
			conventional language-conditioned policies. <Susie /> achieves state-of-the-art results on the
			simulated <a href="http://calvin.cs.uni-freiburg.de/">CALVIN benchmark</a>, and also
			demonstrates robust performance on real-world manipulation tasks, beating
			<a href="https://robotics-transformer-x.github.io/">RT-2-X</a> as well as an oracle policy that
			gets access to ground-truth goal images.
		</p>

		<!-- teaser figure -->
		<div class="flex flex-col items-center mt-8 w-full">
			<div class="w-full lg:w-10/12">
				<img src="{base}/teaser.svg" alt="teaser" />
			</div>
			<p class="italic mt-4">
				<Susie /> alternates generating subgoals using an image-editing diffusion model and executing
				those subgoals using a language-agnostic low-level policy.
			</p>
		</div>

		<div class="mt-8">
			<h2 class="text-2xl">Zero-Shot Manipulation</h2>
			<div class="flex flex-col items-center mt-8 mb-4 w-full">
				<div class="w-full lg:w-10/12">
					<img src="{base}/scenes_combined.svg" class="w-full" alt="teaser" />
				</div>
			</div>
			<p>
				<Susie /> demonstrates state-of-the-art performance in the zero-shot setting of the CALVIN benchmark,
				where the policy is trained on 3 environments (A, B, and C) and tested on a fourth. <Susie
				/> also shows incredibly strong performance in the real world. Scene C is situated on top of
				a table with a tiled surface, which is unlike anything seen in the training data, and requires
				manipulating 4 objects, 3 of which are unseen in the data. This means that the robot must identify
				the novel objects from the language instruction alone while ignoring its affinity for the object
				that is heavily represented in its training data. <Susie /> outperforms all of the baseline methods
				in all of the scenes, including
				<a href="https://robotics-transformer-x.github.io/">RT-2-X</a>, which is a 55 billion
				parameter vision-language-action model trained on a 20x larger superset of <Susie />'s robot
				training data.
			</p>
			<div class="ml-4 mt-2">
				<Collapsible>
					<h3 slot="header" class="text-xl">Simulation Results</h3>
					<CalvinTable slot="body" let:isOpen {isOpen} />
				</Collapsible>
			</div>
		</div>

		<div class="mt-2">
			<div class="ml-4">
				<Collapsible>
					<h3 slot="header" class="text-xl">Real-World Results</h3>
					<RealTable slot="body" let:isOpen {isOpen} />
				</Collapsible>
			</div>
		</div>

		<div class="mt-8">
			<h2 class="text-2xl">Enhanced Precision</h2>
			<Precision />
		</div>

		<div class="mt-8">
			<h2 class="text-2xl">Leveraging Video Data</h2>
			<VideoData />
		</div>
	</div>
</div>

<style>
</style>
