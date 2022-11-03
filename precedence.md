---
layout: "page-layout.webc"
---

# Shadow DOM Styling Precedence

For elements exposed to the Shadow DOM (i.e. the host and slotted
elements) and elements exposed from the Shadow DOM (i.e. parts), this is
the order of precedence the styles take:

## 1. Styles set in the Shadow DOM with `!important`

```html
<style>
	/* All of the following have no effect no matter how specific. */
	article { color: deeppink; }
	h1 { font-weight: 400; }
	::part(container) { border: 1px solid blue; }
</style>
<article>
	<template shadowroot="open">
		<style>
			/* All of the following cannot be overridden outside of the Shadow DOM. */
			:host { color: dodgerblue !important; }
			::slotted(h1) { font-weight: 500 !important; }
			[part="container"] { border: 2px dashed red !important; }
		</style>
		<div part="container">
			<slot></slot>
		</div>
	</template>
	<h1>Hello, World!</h1>
</article>
```

## 2. Styles set in the light DOM

```html
<style>
	/* These will override any Shadow DOM styles. */
	article { color: deeppink; }
	h1 { font-weight: 400; }
	::part(container) { border: 1px solid blue; }
</style>
<article>
	<template shadowroot="open">
		<style>
			/* All of these are overridden by the light DOM styles. */
			:host { color: dodgerblue; }
			::slotted(h1) { font-weight: 500; }
			[part="container"] { border: 2px dashed red; }
		</style>
		<div part="container">
			<slot></slot>
		</div>
	</template>
	<h1>Hello, World!</h1>
</article>
```

## 3. Styles set in the Shadow DOM

```html
<article>
	<template shadowroot="open">
		<style>
			:host { color: dodgerblue; }
			::slotted(h1) { font-weight: 500; }
			[part="container"] { border: 2px dashed red; }
		</style>
		<div part="container">
			<slot></slot>
		</div>
	</template>
	<h1>Hello, World!</h1>
</article>
```
