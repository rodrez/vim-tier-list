<script lang="ts">
	import DropList from './DropList.svelte';
	import ImageDropContainer from './ImageDropContainer.svelte';
	import './app.css';

	let rankings = {
		S: [
			{ id: 1, title: 'I' },
			{ id: 2, title: 'Am' },
			{ id: 3, title: 'Yoda' },
			{ id: 9, title: 'Am' },
			{ id: 11, title: 'Yoda' },
			{ id: 4, title: 'Luke' },
			{ id: 5, title: 'Skywalker' },
			{ id: 6, title: 'Emperor' },
			{ id: 7, title: 'Palpatine' },
			{ id: 8, title: 'Death' },
			{ id: 0, title: 'Star' },
			{ id: 10, title: 'Star' }
		],
		'A+': [
			{ id: 4, title: 'Luke' },
			{ id: 5, title: 'Skywalker' }
		],
		A: [
			{ id: 6, title: 'Emperor' },
			{ id: 7, title: 'Palpatine' },
			{ id: 8, title: 'Death' },
			{ id: 0, title: 'Star' }
		],
		B: [],
		C: [],
		D: []
	};
</script>

<div class=" w/8-12 m-16">
	<div class="flex flex-col gap-y-4">
		<DropList items={rankings['S']} type="light" />
		<DropList className="rounded-l-md bg-gradient-to-r from-[#2d3741] to-[#434e5b] min-h-[148px] w-40" items={rankings['A+']} type="light" />
		<DropList className="rounded-l-md bg-gradient-to-r from-[#4df70c] to-[#07c509] min-h-[148px] w-40" items={rankings['A']} type="light" />
		<DropList className="rounded-l-md bg-gradient-to-r from-[#ffd901] to-[#fdbd21] min-h-[148px] w-40" items={rankings['B']} type="light" />
		<DropList className="rounded-l-md bg-gradient-to-r from-[#f09400] to-[#fc5b00] min-h-[148px] w-40" items={rankings['C']} type="light" />
		<DropList className="rounded-l-md bg-gradient-to-r from-[#a20202] to-[#c21e24] min-h-[148px] w-40" items={rankings['D']} type="light" />
	</div>
	<!-- Our container that holds the images -->
	<div class="mt-8 flex min-h-[296px] bg-slate-700 w-full rounded-md">
		<h2 class="text-slate-100 text-2xl font-semibold mt-4 ml-4">To be Ranked</h2>
		<div data-id="to-be-ranked-container" />
        <ImageDropContainer />
	</div>
</div>
