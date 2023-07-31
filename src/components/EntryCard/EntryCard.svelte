<script>
	import { onDestroy } from "svelte";

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
	<div>
	  <img src={imagePreviewUrl} alt="Preview" />
	</div>
	<p>Filename: {file.name}</p>
  {/if}
  