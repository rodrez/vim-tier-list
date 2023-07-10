<script lang="ts">
	import { dndzone } from 'svelte-dnd-action';
	import { flip } from 'svelte/animate';

    type Item = {
        id: number,
        title: string
        }

	const flipDuration = 200;

	export let items: Item[] = [];
	export let type: string;
	export let className = '';

	function handleSort(e: any) {
		items = e.detail.items;
	}
</script>

<div class="flex">
	<div class={className || "rounded-l-md bg-gradient-to-r from-[#0381d9] to-[#1b4090] min-h-[148px] w-40"} />
	<section
		class="rounded-r-md bg-slate-700 min-h-[148px] w-full flex flex-wrap gap-4 items-center p-4"
		use:dndzone={{ items, flipDuration, type }}
		on:consider={handleSort}
		on:finalize={handleSort}
	>
		{#each items as item (item.id)}
			<div
                class="h-24 w-24 text-white bg-slate-500 flex items-center justify-center"
				style={type === 'dark' ? 'background-color:rgba(0,0,0,0.7); color: white' : ''}
				animate:flip={{ duration: flipDuration }}
			>
				{item.title}
			</div>
		{/each}
	</section>
</div>
