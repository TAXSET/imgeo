<script>
	import EntryCard from '../components/EntryCard/EntryCard.svelte';
	import Map from "../components/Map/Map.svelte"

	/**
	 * Svelte component to select and display images.
	 * @component
	 */

	/**
	 * Array to store selected files.
	 * @type {Array<File>}
	 */
	let selectedFiles = [];

	/**
	 * Handles the file change event when a new image file is selected.
	 * Updates the `selectedFile` variable with the chosen image file.
	 * @param {any} event - The file change event.
	 */
	const handleFileChange = (event) => {
		/**
		 * @type {FileList}
		 */
		selectedFiles = Array.from(event?.target.files);
	};
</script>

<div class="prose w-11/12 container mx-auto max-w-screen-2xl">
	<div class="grid grid-cols-12 gap-4">
		<div class="col-span-3 overflow-y-scroll max-h-screen">
			<h2>Files</h2>

			<h4>Currently editing</h4>

			<div class="grid grid-cols-6">
				{#each selectedFiles as file, index}
					<EntryCard {file} {index} />
				{/each}
			</div>

			<input
				type="file"
				multiple
				class="file-input w-full max-w-xs"
				accept="image/*"
				on:change={handleFileChange}
			/>
		</div>
		<div class="col-span-9">
			<h2>Select location</h2>
			<Map />
		</div>
	</div>
</div>