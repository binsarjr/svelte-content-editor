<script lang="ts">
	import { onMount } from 'svelte';

	export let html: string = '';
	export let placeholder: string = '';

	let element: HTMLDivElement;
	const elementClass = '__inlineEditor_' + Math.floor(Math.random() * 9999999999999);

	// make div element keep can click when data is empty
	$: if (html == '' || /^<br\/?>$/.test(html)) {
		if (placeholder) html = placeholder;
		else html = '&nbsp;';
	}

	function onClick(e: MouseEvent) {
		if (placeholder === html) {
			document.execCommand('selectAll', false);
		}
	}

	onMount(() => {
		document.querySelector('.' + elementClass)?.addEventListener('keydown', function (_e) {
			const e = _e as KeyboardEvent;
			const enter = e.keyCode === 13;
			const shiftEnter = e.keyCode === 13 && e.shiftKey;
			if (enter || shiftEnter) {
				e.preventDefault();
			}
		});
	});
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div
	contenteditable
	class={elementClass}
	class:italic={html === placeholder}
	bind:this={element}
	bind:innerHTML={html}
	on:click={onClick}
/>

<style>
	.italic {
		font-style: italic;
	}
</style>
