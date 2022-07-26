<script context="module">
    export const key = Symbol('toolbar');
</script>

<script lang="ts">
    import MenuItem from './ToolbarItem.svelte';
    import { setContext } from 'svelte';
    import { writable } from 'svelte/store';

    const nav = writable([]);

    setContext(key, nav);

    // this is the nested object we use (instead of svelte components)
    export let menu: any[];

    let activeMenu = -1;

    // only focus header if we click a non-spacer
    let headerFocused = false;
    let spacerEl: HTMLElement;
    function handleHeaderClick(e) {
	if (e.target == spacerEl) return;
	headerFocused = true
    }

    // if we click outside the menu, close it
    let headerEl: HTMLElement;
    function possiblyCloseMenu(e) {
	if (e.target == headerEl || headerEl.contains(e.target)) return;
	headerFocused = false;
    }
</script>

<style>
    header {
	user-select: none;
	display: grid;
	color: white;
    }
    header :global(div > span) { 
	background: #222;
    }
    span {
	background: #333;
    }
</style>

<svelte:window on:click={possiblyCloseMenu} />

<header 
    style="grid-template-columns: {'auto '.repeat(menu.length)}1fr;" 
    bind:this={headerEl} 
    on:click={handleHeaderClick}>
    {#each menu as menuItem, i}
	<MenuItem
		root={true} 
		menu={menuItem} 
		expanded={i === activeMenu && headerFocused} 
		on:mouseenter={() => activeMenu = i} />
    {/each}
    <span bind:this={spacerEl} />
</header>
