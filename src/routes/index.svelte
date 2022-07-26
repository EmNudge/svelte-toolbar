<script lang="ts">
    import Toolbar from '../lib/Toolbar.svelte';

    const logger = (text: string) => () => console.log(text);
    const save = logger('save');
    const close = logger('close');
    const doThing = logger('doThing');
    const doOtherThing = logger('doOtherThing');
</script>

<Toolbar>
    <ToolbarItem name="File">
	<ToolbarItem name="Save As..." on:click={save} />
	<ToolbarItem name="Close" on:click={close} />
    </ToolbarItem>
    <ToolbarItem name="Edit">
	<ToolbarItem name="Do Thing" on:click={doThing} />
	<ToolbarItem name="Do Other Thing" on:click={doOtherThing} />
    </ToolbarItem>
</Toolbar>

<h1>Toolbar Playground</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
