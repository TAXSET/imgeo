<script>
	import EntryCard from "../components/EntryCard/EntryCard.svelte";

/**
   * Represents an ImageInput Svelte component that allows the user to select an image file.
   * @module ImageInput
   */

  /**
   * The selected image file.
   * @type {File | undefined}
   */
   let selectedFile;

/**
 * Handles the file change event when a new image file is selected.
 * Updates the `selectedFile` variable with the chosen image file.
 * @param {any} event - The file change event.
 */
const handleFileChange = (event) => {
  const file = event?.target.files[0];
  if (file && file.type.startsWith('image/')) {
	selectedFile = file;
  } else {
	selectedFile = undefined;
  }
};
</script>
<div class="prose w-11/12 container mx-auto max-w-screen-2xl">
	<div class="grid">
		<div class="col-span-2">
			<h2>Files</h2>
			<EntryCard
				file = {selectedFile}
			/>
			<input type="file" accept="image/*" on:change={handleFileChange} />
		</div>
		<div class="col">
			<p>Test</p>
		</div>
	</div>
</div>