<script lang="ts">
	import { onMount } from 'svelte';

	export let value = '';
	/**
	 * if true you will get html format
	 */
	export let html = false;
	export let placeholder = '';

	let element: HTMLDivElement;
	const elementClass = '__inlineEditor_' + Math.floor(Math.random() * 9999999999999);

	// make div element keep can click when data is empty
	$: if (value == '' || /^<\s{0,}br\s{0,}\/?\s{0,}>$/.test(value)) {
		if (placeholder) value = placeholder;
		else value = '&nbsp;';
	}

	function onClick(e: MouseEvent) {
		if (placeholder === value) {
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
	class:italic={value === placeholder}
	class:text-only={!html}
	bind:this={element}
	bind:innerHTML={value}
	on:click={onClick}
/>

<style>
	.italic {
		font-style: italic;
	}
	.text-only {
		white-space: pre-wrap;
	}
</style>
