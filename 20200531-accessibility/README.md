# Dangers of using WAI-ARIA incorrectly

**Source**: [The Dangers of Using WAI-ARIA Incorrectly](https://seesparkbox.com/foundry/using_wai-aria_aria-hidden_aria-label_aria-live_correctly)
by Anastasia Lanz

WAI-ARIA stands for "Web Accessibility Initiative – Accessible Rich Internet Application"

----

## Avoid repurposing HTML elements when other native elements already have the behavior you need.

Avoid doing things like using a `<div>` because it's easier to style than a `<button>`.
A couple of downsides to using a `<div>` are `<divs>` are not focusable by default and `<div>` will 
have to be given the role of `button`.

## Adding redundant roles to elements

Bad:

```html
<button role="button">Cancel</button>
<h1 role="header">ARIA is great</h1>
```

Good:

```html
<button>Cancel</button>
<h1>ARIA is great</h1>
```

## Inadvertently overriding semantics

One of the second rules of ARIA from the "Using ARIA Document" says "Do not change native semantics,
unless you really have to."

Bad:

```html
<h1 role="button">A heading</h1>
```

Good:

```html
<h1><button>A heading</button></h1>
```

## Using `aria-hidden` inappropriately

When using `aria-hidden="true"`, make sure it's not a focusable element. It is possible for it to be
removed from the accessibility tree, but still be focusable by keyboard.

To fix this issue, `tabindex="-1"` can be used.

Bad:

```html
<button aria-hidden="true">Button text</button>
```

Good:

```html
<button tabindex="-1" aria-hidden="true">Button text</button>
```

## Using `aria-live` Inappropriately
`aria-live` is used to announce page changes to screen reader users.

Bad:

```html
<body aria-live="assertive">
```

This is bad because every change that happens within the `<body>` tag will be ready by teh screen 
reader and will interrupt the user.

Good:

Use selectively on elements that contain changes you want to announce.

```html
<div aria-live="polite"><!-- announcement updates here --></div>
```

Deque University has an `aria-live` [playground](https://dequeuniversity.com/library/aria/liveregion-playground).


