<script lang="ts">
	import Editor from '$lib/Editor.svelte';
	import InlineEditor from '$lib/InlineEditor.svelte';
	let html = '';
</script>

<h1>Welcome to your library project</h1>
<p>Create your package using @sveltejs/package and preview/showcase your work with SvelteKit</p>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<p>ISI Inline Editor: {html}</p>
<InlineEditor bind:value={html} placeholder="Klik disini" />

<h2>Editor</h2>
<Editor html="ini editor" />
