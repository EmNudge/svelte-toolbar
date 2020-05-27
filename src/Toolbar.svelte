<script>
  import MenuItem from './ToolbarItem.svelte';
  
	// this is the nested object we use (instead of svelte components)
	export let menu;
	
  let activeMenu = -1;
	
	// only focus header if we click a non-spacer
  let headerFocused = false;
	let spacerEl;
	function handleHeaderClick(e) {
		if (e.target == spacerEl) return;
		headerFocused = true
	}
	
	// if we click outside the menu, close it
	let headerEl;
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