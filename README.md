# Svelte Toolbar

This was created when looking for a proper way to display a user-navigable menu.
This emulates the toolbar menu you would find on products like VS-Code. 

Unfortunately, the CSS is not easily changeable. If you have ideas for how to remedy this, you can leave them in an issue. For now, you can simply copy/paste the code and just change the CSS.

## Usage
```html
<script>
  import Toolbar from 'svelte-toolbar';
  // snip...
  const menu = [
    { name: 'File', children: [
      { name: 'Save As...', action: saveItem },
      { name: 'Close', action: closeFile },
    ]},
    { name: 'Edit', children: [
      { name: 'Do Thing', action: doThing },
      { name: 'Do Other Thing', action: doOtherThing }
    ]}
    // etc...
  ]
</script>

<Toolbar {menu} />
```
**Note**: Any menu item can have an action or children. Probably both, but it shouldn't.

## How does this differ from a CSS Dropdown Menu?
1. A menu is generated from a nested object rather than annoying hand-crafted HTML
2. Top-level menus are only expanded when one of the top-level items are clicked.
3. Top-level menus will stay open until the user clicks outside of the toolbar.

