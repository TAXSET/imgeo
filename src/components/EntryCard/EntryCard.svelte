<script>
	import { onDestroy } from 'svelte';

	/**
	 * Represents an ImagePreview Svelte component that displays the image preview and filename of a given file.
	 * @module ImagePreview
	 */

	/**
	 * The file to be previewed.
	 * @type {File | undefined}
	 */
	export let file;

	/**
	 * Index of the entry.
	 * @type {Number}
	 */
	export let index;

	/**
	 * The base64 data URL of the selected image for preview.
	 * @type {string | undefined}
	 */
	let imagePreviewUrl;

	/**
	 * Updates the image preview URL whenever the `file` prop changes.
	 */
	$: {
		if (file) {
			const reader = new FileReader();
			reader.onload = (e) => {
				imagePreviewUrl = e?.target?.result?.toString(); // Convert ArrayBuffer to string
			};
			reader.readAsDataURL(file);
		} else {
			imagePreviewUrl = undefined;
		}
	}

	/**
	 * Clean up the object URL when the component is destroyed to free up resources.
	 */
	onDestroy(() => {
		if (imagePreviewUrl) {
			URL.revokeObjectURL(imagePreviewUrl);
		}
	});
</script>

{#if file && imagePreviewUrl}
	{#if index == 0}
		<div class="col-span-6 mb-5">
			<img src={imagePreviewUrl} alt="Preview" class="m-0" />
			<h5 class="mt-0">{file.name}</h5>
		</div>
	{:else}
		<div class="col-span-3">
			<img src={imagePreviewUrl} alt="Preview" class="m-0" />
		</div>
	{/if}
{/if}
