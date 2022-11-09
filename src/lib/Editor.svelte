<script lang="ts">
	export let html: string;
	export let tinggi = '78vh';
	$: if (html == '') {
		html = '&nbsp;';
	}
	function block(x: string) {
		document.execCommand('formatBlock', false, x);
	}
	function sebagian(x: string) {
		document.execCommand(x, false);
	}
	function link(x: string) {
		const url = prompt('Enter Link');
		if (!url) {
			alert('No Link Founded');
			return;
		}
		document.execCommand(x, false, url);
	}
</script>

<hr />
<div>
	<button on:click|preventDefault={() => block('h1')} class="btn btn-success">H1</button>
	<button on:click|preventDefault={() => block('h2')} class="btn btn-success">H2</button>
	<button on:click|preventDefault={() => block('h3')} class="btn btn-success">H3</button>
	<button on:click|preventDefault={() => block('h4')} class="btn btn-success">H4</button>
	<button on:click|preventDefault={() => block('p')} class="btn btn-success">P</button>
	<button on:click|preventDefault={() => sebagian('bold')} class="btn btn-success">Bold</button>
	<button on:click|preventDefault={() => sebagian('italic')} class="btn btn-success">Italic</button>
	<button on:click|preventDefault={() => link('createLink')} class="btn btn-success">Link</button>
	<button on:click|preventDefault={() => sebagian('unlink')} class="btn btn-success">Unlink</button>
	<button on:click|preventDefault={() => link('insertImage')} class="btn btn-success">Image</button>
	<button on:click|preventDefault={() => sebagian('insertOrderedList')} class="btn btn-success"
		>List Number</button
	>
	<button on:click|preventDefault={() => sebagian('insertUnorderedList')} class="btn btn-success"
		>List Bullet</button
	>
</div>
<hr />
<div contenteditable bind:innerHTML={html} style="max-height: {tinggi}" />
<hr />

<style type="text/css">
	button {
		margin-bottom: 0.3em;
	}
	div {
		overflow: auto;
	}
</style>
