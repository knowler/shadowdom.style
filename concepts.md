---
layout: "page-layout.webc"
---

# Concepts

- Understanding the Shadow Root and its host
- Understanding slots
- Understanding parts
- What is in the Shadow DOM and what is outside of the Shadow DOM.

## Shadow DOM Concepts

### Shadow Roots

The Declarative Shadow DOM isn’t available in all browsers. For
examples, it provides a much easier syntax to grok, so we’ll use it
throughout the site.

```html
<article>
	<template shadowroot="open">
	</template>
</article>
```

### Slots

Slots are a feature of the Shadow DOM that allow light DOM children
within the host element to be “projected” into the Shadow DOM. That’s
important to grasp. The elements are not being relocated. They still
exist in the light DOM. You can access these elements for styling with
the `::slotted()` pseudo-element selector.

### Parts

Parts are a feature of the Shadow DOM that allow Shadow DOM elements to
be exposed to the light DOM for styling. You can access these elements
with the `::part()` pseudo-element selector.

## Important CSS Concepts

### Inheritance

It’s important to understand inheritance in CSS, because it affects the
Shadow DOM. For example, `font-family` is a property that inherits by
default.

### CSS Custom Properties

It’s important to understand that the default value of a custom property
is `inherit`. This means that CSS custom properties will “pierce”
throught the Shadow DOM divide by default.

In the future we’ll be able to explicitly set if a custom property
should inherit by default.

```css
@property --my-color {
	syntax: "<color>";
	inherits: false;
	initial-value: red;
}
```
