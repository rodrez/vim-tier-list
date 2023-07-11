<script lang="ts">
	import Dropzone from 'svelte-file-dropzone/Dropzone.svelte';
	import { dndzone } from 'svelte-dnd-action';

	export let images: { accepted: File[]; rejected: File[] } = {
		accepted: [],
		rejected: []
	};

	type DropEvent = CustomEvent<{
		acceptedFiles: File[];
		fileRejections: File[];
	}>;

	function handleImagesSelect(e: DropEvent) {
		const { acceptedFiles, fileRejections } = e.detail;
		let accepted = [...images.accepted, ...acceptedFiles];
		let rejected = [...images.rejected, ...fileRejections];

		images = { accepted, rejected };
	}

	function removeFromAccepted(image: File) {
		if (image) {
			const updatedAccepted = images.accepted.filter(
				(item) => item?.lastModified !== image?.lastModified
			);
			images.accepted = updatedAccepted;
		}
	}
	function handleSort(e: any) {
		items = e.detail.items;
	}

</script>

<div class="flex flex-col" data-id="to-be-ranked-container">
	<div>
		<Dropzone inputElement accept="image/png, image/jpeg, image/gif" on:drop={handleImagesSelect}>
			<p>Drop Images Here</p>
		</Dropzone>
	</div>
	<div
		use:dndzone={{ images['accepted'] }}
		on:consider={handleSort}
		on:finalize={handleSort}

    class="border-2 border-red-400 h-52 flex flex-wrap gap-4 p-4">
		{#each Array.from(images.accepted) as image}
			<div class="relative w-16 h-16">
				<img src={URL.createObjectURL(image)} class="" alt="img" />
				<div class="absolute -top-2 -right-2">
					<button
						on:click={() => removeFromAccepted(image)}
						type="button"
						class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ml-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white"
						data-modal-hide="defaultModal"
					>
						<svg
							class="w-3 h-3"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 14 14"
						>
							<path
								class="stroke-red-500"
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"
							/>
						</svg>
						<span class="sr-only">Close modal</span>
					</button>
				</div>
			</div>
		{/each}
	</div>
</div>
