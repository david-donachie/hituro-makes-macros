## The tabs macro ##

The `<<tabs>>` macro creates a simple tabbed area, where content is shown and hidden by clicking on the tabs.

<img width="664" alt="Screenshot 2023-02-09 at 18 05 27" src="https://user-images.githubusercontent.com/4206142/217899873-601fe0a8-33e3-4c95-9c7d-d9feee4d86c4.png">

### Installation ###

Add the contents of [tabs.js](tabs.js) to your story Javascript, and the contents of [tabs.css](tabs.css) to your story Stylesheet.

### Syntax ###

```html
<<tabs>>
    <<tab "Potions">>
    POTIONS!
    <<tab "Items">>
    ITEMS!
    <<tab "Keys">>
    KEYS!
<</tabs>>
```

#### `<<tabs>>` ####

The `<<tabs>>` macro must contain one or more `<<tab>>` macros, defining both the tabs to be displayed, and the content of the tabs. The content has leading and trailing whitespace trimmed, but is otherwise treated as normal passage content.

The tabs macro takes an optional string argument, which will generate the id of the tabs wrapper element.

#### `<<tab>>` ####

The `<<tab>>` macro has a mandatory first argument, which is the name displayed on the tab. The name is also used to generate the id of the content area corresponding to the tab (which is of the form `tabs-content-NAME` where `NAME` is the tab name, converted to lowercase, spaces turned into `-`, and non-alphanumeric characters removed.)

The tab macro takes an optional second argument. If this evaluates to true, the tab will be selected when the tab-group is displayed. If no tab is pre-selected, then the first tab is displayed.

Note: if the optional id argument is passed to `<<tabs>>` the same id will be prepended to the id of any tabs it contains: e.g. `id-tabs-content-NAME`.

### Generated HTML and CSS ###

The example above would generate the following HTML.

```html
<div class="tabs-tabset" style="--cols:3">
	<div class="tabs-tabs">
		<button id="tabs-contents-potions-control" type="button" role="button" tabindex="0" class="selected">Potions</button>
		<button id="tabs-contents-items-control" type="button" role="button" tabindex="0">Items</button>
		<button id="tabs-contents-keys-control" type="button" role="button" tabindex="0">Keys</button>
	</div>
	<div class="tabs-contents">
		<div class="tabs-content" id="tabs-contents-potions">POTIONS!</div>
		<div class="tabs-content hidden" id="tabs-contents-items">ITEMS!</div>
		<div class="tabs-content hidden" id="tabs-contents-keys">KEYS!</div>
	</div>
</div>
```

Some of the basic styling of the tab group can be controlled with CSS variables, as follows:

```css
  --button-rounding: 10px; /* the radius of the top-corners of the buttons */
  --tab-color: #343434;    /* the background color of a tab */
  --tab-selected: #565656; /* the background color of the selected tab */
```

### Examples ###

A tab set with the second tab selected by default
```html
<<tabs>>
    <<tab "Potions">>
    POTIONS!
    <<tab "Items" true>>
    ITEMS!
    <<tab "Keys">>
    KEYS!
<</tabs>>
```

A tab set with a custom id
```html
<<tabs "inventory">>
    <<tab "Potions">>
    POTIONS!
    <<tab "Items">>
    ITEMS!
    <<tab "Keys">>
    KEYS!
<</tabs>>
```
