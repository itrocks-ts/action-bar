[![npm version](https://img.shields.io/npm/v/@itrocks/action-bar?logo=npm)](https://www.npmjs.org/package/@itrocks/action-bar)
[![npm downloads](https://img.shields.io/npm/dm/@itrocks/action-bar)](https://www.npmjs.org/package/@itrocks/action-bar)
[![GitHub](https://img.shields.io/github/last-commit/itrocks-ts/action-bar?color=2dba4e&label=commit&logo=github)](https://github.com/itrocks-ts/action-bar)
[![issues](https://img.shields.io/github/issues/itrocks-ts/action-bar)](https://github.com/itrocks-ts/action-bar/issues)
[![discord](https://img.shields.io/discord/1314141024020467782?color=7289da&label=discord&logo=discord&logoColor=white)](https://25.re/ditr)

# action-bar

CSS for action button bars with flexible layout and basic styling.

*This documentation was written by an artificial intelligence and may contain errors or approximations.
It has not yet been fully reviewed by a human. If anything seems unclear or incomplete,
please feel free to contact the author of this package.*

## Installation

```bash
npm i @itrocks/action-bar
```

Include the generated CSS in your HTML, either directly from `node_modules`
or via your usual bundler / asset pipeline.

```html
<link href="./node_modules/@itrocks/action-bar/action.css" rel="stylesheet">
```

## Usage

`@itrocks/action-bar` provides a small set of CSS classes to display
action buttons as a flexible horizontal bar.

At its core, you:

1. Wrap your actions in a `<ul class="actions">` list.
2. Put each action inside a `<li>` element.
3. Use a clickable element (`<button>`, `<a>`, `<input type="submit">`,
   etc.) inside each `<li>`.

The stylesheet takes care of:

- horizontal layout with wrapping when there is not enough space,
- basic button look (border, background, hover effect),
- consistent padding so there is room for an optional icon on the left.

### Minimal example

```html
<link href="./node_modules/@itrocks/action-bar/action.css" rel="stylesheet">

<ul class="actions">
	<li><button type="submit" name="save">Save</button></li>
	<li><button type="submit" name="cancel">Cancel</button></li>
</ul>
```

This renders two buttons side by side, with a small gap between them and a
neutral default styling.

### Example with general / selection bars and icons

In a typical it.rocks application you often have two distinct action bars:

- a **general** bar for actions that apply to the whole page,
- a **selection** bar for actions that apply to the current selection
  (for example selected rows in a table).

```html
<link href="./node_modules/@itrocks/action-bar/action.css" rel="stylesheet">

<!-- General actions at the top of a page -->
<ul class="actions general">
	<li>
		<button type="button" class="new" style="background-image: url('/icons/add.svg')">
			New
		</button>
	</li>
	<li>
		<button type="submit" class="search" style="background-image: url('/icons/search.svg')">
			Search
		</button>
	</li>
</ul>

<!-- Selection‑based actions below a list or table -->
<ul class="actions selection">
	<li>
		<button type="submit" class="delete" style="background-image: url('/icons/delete.svg')">
			Delete selected
		</button>
	</li>
</ul>
```

Only the layout and base look (padding, border, hover background) come from
`@itrocks/action-bar`; the icon is provided by a `background-image` (inline
style in the example above, but most projects use dedicated CSS classes
instead).

## API

The package exposes a single stylesheet, `action.css`, which defines a few
CSS selectors. There is no JavaScript API.

### `ul.actions`

Turns an unordered list into a horizontal action bar.

- Display: `flex` with wrapping enabled (`flex-wrap: wrap`).
- Spacing: `gap: 5px`, `padding: 5px`, no default margin.
- Intended children: `<li>` elements, each containing one clickable
  element.

#### `ul.actions.general`

General action bar, usually displayed at the top of a page or card.

- Adds a bottom border: `border-bottom: 1px solid #ccc`.

#### `ul.actions.selection`

Selection‑based action bar, usually displayed below a list or table
to act on the current selection.

- Adds a top border: `border-top: 1px solid #ccc`.

### `.action`

Generic class for standalone actions or for use on the clickable element
inside an action bar.

- Pointer cursor.
- Base padding: `4px 8px 4px 26px` (left padding keeps room for an icon).
- Line height: `16px`.

You can apply `.action` on:

- a button that is not inside a `.actions` list but should look the
  same as the others;
- an `<input type="submit">` rendered by other components (for example
  the `search` submit button in the movie search form of this project).

### Shared styles for `.action` and `ul.actions > li`

Both standalone actions and list items share the same visual treatment:

- white background,
- 1‑pixel grey border with a small radius,
- inline‑block display,
- smooth background hover transition,
- support for an optional background icon:
  - `background-position: left center`,
  - `background-repeat: no-repeat`,
  - `background-size: 24px`.

You are expected to provide the icon yourself by setting
`background-image` (directly or via a custom CSS class).

### `ul.actions > li > *`

Normalises the content of each list item (typically a link, button
or input):

- same line height and padding as `.action` (`4px 8px 4px 26px`).

### `ul.actions > li > a`

Ensures links inside an action bar behave like buttons:

- displayed as `inline-block` so that padding and hover styles apply
  properly.

### `ul.actions > li > input`

Resets the browser’s default styling for inputs so they match other
actions:

- transparent background,
- no border,
- pointer cursor.

## Typical use cases

- Grouping several **form submit** buttons (search, save, reset, export)
  into a consistent horizontal bar.
- Displaying **page‑level actions** (new, duplicate, delete, back) at the
  top or bottom of an entity screen.
- Providing **selection actions** below a table or list (delete selected,
  export selected, mark as read, etc.).
- Styling a few **standalone buttons** with the same look as the global
  action bars by simply applying the `.action` class.
- Integrating with the rest of the it.rocks UI stack, for example in
  association with `@itrocks/list`, `@itrocks/edit` or custom pages
  that need a compact, reusable action area.
