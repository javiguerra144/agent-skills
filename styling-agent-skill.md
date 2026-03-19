# Skill: Style UI Using BEM

## Purpose

Use this skill when the user wants UI code styled or organized using the BEM methodology.

This skill helps the agent:

* write HTML, templates, JSX, or component markup with BEM class names
* create or refactor CSS/SCSS to follow BEM conventions
* rename inconsistent selectors into a predictable structure
* document and enforce a maintainable naming system for UI styling

---

## When to Use

Use this skill when the user asks to:

* style a UI using BEM
* refactor CSS to BEM
* create maintainable class names
* organize component styles
* convert ad hoc selectors into a naming convention
* make front-end code easier to scale

Do **not** use this skill when:

* the user explicitly wants utility-first styling only
* the codebase already follows another required convention
* the task is about CSS-in-JS patterns that do not use class names
* the request is unrelated to UI structure or selector naming

If the repo already has a naming convention, align with it unless the user asked for a BEM migration.

---

## Core Rules

1. Use BEM names consistently: `block`, `block__element`, `block--modifier`.
2. Keep block names independent and meaningful.
3. Use elements only when they are part of a block.
4. Use modifiers for variations in appearance or state, not for unrelated structure.
5. Do not chain selectors deeply when a BEM class can express intent directly.
6. Avoid styling raw tags when a block or element selector is more appropriate.
7. Prefer flat, readable selectors over clever nesting.
8. Preserve behavior while refactoring names.
9. Avoid inventing abstractions the markup does not need.
10. Keep class names semantic to the UI role, not to visual trivia.

---

## BEM Quick Reference

### Block

A standalone UI component.

Examples:

* `card`
* `navbar`
* `modal`
* `product-tile`

### Element

A part of a block that has no standalone meaning outside that block.

Examples:

* `card__title`
* `navbar__item`
* `modal__footer`

### Modifier

A flag that changes appearance, behavior, or state.

Examples:

* `card--featured`
* `navbar__item--active`
* `modal--fullscreen`

---

## Naming Rules

### Block Names

* use lowercase
* use hyphenated words if needed
* keep names based on component meaning

Good:

* `user-menu`
* `search-form`
* `checkout-summary`

Avoid:

* `blue-box`
* `left-panel-big`
* `text123`

### Element Names

* always belong to a block
* use `__` once between block and element
* reflect responsibility inside the block

Good:

* `tabs__list`
* `tabs__tab`
* `tabs__panel`

Avoid:

* `tabs__list__item`
* `tabs .item`
* `item` without block context

### Modifier Names

* use `--` for variants or states
* apply to block or element
* describe a meaningful change

Good:

* `button--primary`
* `button--disabled`
* `accordion__section--expanded`

Avoid:

* `button--div`
* `card--margin20`
* `title--left`

---

## Agent Workflow

### 1) Identify UI Components

Break the UI into standalone blocks.

Ask implicitly:

* what components exist?
* what parts belong to each component?
* which styles are shared vs local?

Example:
A product page may include:

* `product-card`
* `price-badge`
* `review-list`
* `add-to-cart-form`

### 2) Map Internal Parts to Elements

For each block, identify its internal structure.

Example:
`product-card` may contain:

* `product-card__image`
* `product-card__title`
* `product-card__price`
* `product-card__actions`

### 3) Identify Variants and States

Use modifiers only for meaningful differences.

Examples:

* `product-card--featured`
* `product-card__button--loading`
* `tabs__tab--active`

Do not use modifiers for layout hacks when a layout wrapper or parent context would be cleaner.

### 4) Refactor Selectors

Replace ambiguous selectors such as:

* `.container .title`
* `.box.red`
* `.left .btn.active`

With BEM selectors such as:

* `.profile-card__title`
* `.alert.alert--error`
* `.sidebar__button.sidebar__button--active`

### 5) Keep Scope Local

Each block should encapsulate its own elements.

Prefer:

```css
.card {}
.card__title {}
.card__actions {}
```

Over:

```css
.page .content .card h2 {}
.page .content .card .actions {}
```

---

## HTML / JSX Authoring Guidance

### Basic Example

```html
<article class="card card--featured">
  <img class="card__image" src="/img/item.jpg" alt="Item preview" />
  <h2 class="card__title">Premium Plan</h2>
  <p class="card__description">Best for growing teams.</p>
  <div class="card__actions">
    <button class="card__button card__button--primary">Choose plan</button>
  </div>
</article>
```

### React / JSX Example

```jsx
export function Alert({ title, message, type = 'info' }) {
  return (
    <section className={`alert alert--${type}`}>
      <h2 className="alert__title">{title}</h2>
      <p className="alert__message">{message}</p>
      <button className="alert__dismiss">Dismiss</button>
    </section>
  );
}
```

### State Handling

When using JS frameworks, keep state classes predictable.

Good:

* `tabs__tab tabs__tab--active`
* `menu menu--open`
* `input-group__field input-group__field--invalid`

Avoid mixing unrelated state labels without structure.

---

## CSS / SCSS Authoring Guidance

### Plain CSS Example

```css
.card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 16px;
}

.card--featured {
  border-width: 2px;
}

.card__title {
  margin: 0 0 8px;
  font-size: 1.25rem;
}

.card__actions {
  margin-top: 16px;
}

.card__button--primary {
  font-weight: 600;
}
```

### SCSS Example

Use nesting lightly so the compiled selectors remain true BEM selectors.

```scss
.card {
  padding: 1rem;

  &--featured {
    border-width: 2px;
  }

  &__title {
    margin-bottom: 0.5rem;
  }

  &__actions {
    margin-top: 1rem;
  }

  &__button {
    &--primary {
      font-weight: 600;
    }
  }
}
```

Do not overnest beyond what preserves clarity.

---

## Decision Rules

### When Something Should Be a Block

Make it a block if it:

* can conceptually stand alone
* may be reused in other contexts
* has its own internal structure
* has styles not tightly coupled to a parent block

Examples:

* `dropdown`
* `tooltip`
* `comment`

### When Something Should Be an Element

Make it an element if it:

* exists only as part of the parent block
* has no clear meaning outside the block
* is styled in relation to the block’s structure

Examples:

* `dropdown__item`
* `tooltip__arrow`
* `comment__author`

### When Something Should Be a Modifier

Make it a modifier if it:

* changes look, size, theme, or state
* keeps the same base meaning
* should coexist with the base class

Examples:

* `badge--success`
* `button--small`
* `accordion__panel--hidden`

---

## Anti-Patterns to Avoid

* deep descendant selectors like `.page .sidebar ul li a`
* element-of-element naming like `card__header__title`
* visual naming like `green-text` or `big-box`
* using modifiers without the base class
* creating blocks for tiny fragments that are only one text node
* overloading modifiers to represent unrelated concepts
* mixing multiple naming systems in the same component

Bad:

```css
.page .hero .title {}
.box.red {}
.widget .header .title {}
```

Better:

```css
.hero__title {}
.box.box--error {}
.widget__title {}
```

---

## Refactor Pattern

When converting existing UI code to BEM:

1. identify component boundaries
2. rename classes by block
3. map children to elements
4. convert variant/state classes to modifiers
5. reduce descendant selector dependence
6. update markup and styles together
7. verify no behavior or JS hooks break

If JavaScript depends on classes, either:

* update the selectors carefully, or
* preserve separate JS hook classes when needed

Prefer dedicated JS hooks such as:

* `js-modal-close`
* `data-role="modal-close"`

Instead of binding behavior to presentation classes when possible.

---

## Output Modes

Choose based on the task.

### Mode A: New UI Styling

Produce markup and styles already structured with BEM.

### Mode B: Refactor Existing UI

Convert existing class names and selectors to BEM while preserving behavior.

### Mode C: Naming Audit

Review a component and suggest a BEM naming map.

### Mode D: Style Guide

Produce a short team-facing BEM convention document for the repo.

---

## Quality Checklist

Before finalizing, verify:

* every element belongs to a real block
* modifiers are meaningful and not replacing structure
* class names are consistent across markup and styles
* selectors are flatter and clearer than before
* no element-of-element chains were introduced
* reusable components are blocks, not buried descendants
* JS-dependent selectors were handled safely
* naming reflects semantics, not incidental visuals

---

## Example Transformations

### Example 1

Before:

```html
<div class="pricing-box highlighted">
  <h2 class="title">Pro</h2>
  <button class="btn active">Buy now</button>
</div>
```

After:

```html
<div class="pricing-card pricing-card--highlighted">
  <h2 class="pricing-card__title">Pro</h2>
  <button class="pricing-card__button pricing-card__button--active">Buy now</button>
</div>
```

### Example 2

Before:

```css
.sidebar .menu li a.selected {}
```

After:

```css
.sidebar-menu__link.sidebar-menu__link--selected {}
```

### Example 3

Before:

```html
<section class="profile">
  <img class="avatar" />
  <span class="name"></span>
</section>
```

After:

```html
<section class="profile-card">
  <img class="profile-card__avatar" alt="" />
  <span class="profile-card__name"></span>
</section>
```

---

## Safe Failure Behavior

If only partial UI code is available:

* document the visible component structure only
* avoid inventing missing states or variants
* state what was inferred vs directly observed

Examples:

* “I renamed the visible selectors into BEM, but I could not verify whether additional JS relies on the old class names.”
* “This appears to be a single reusable card block with two internal elements; no modifiers were added because no supported variants were shown.”

Do not fabricate:

* hidden states not present in the code
* reusable abstractions without evidence
* accessibility support that is not implemented
* framework conventions the project does not use

---

## Deliverable Patterns

Use one of these depending on the request:

### Full Component Rewrite

Return updated markup and CSS using BEM.

### Class Naming Map

Return a before/after mapping of old selectors to BEM selectors.

### Patch-Oriented Refactor

Return the exact replacement code with minimal surrounding explanation.

### Team Convention Doc

Return a concise style guide the team can adopt.

---

## Default Tone

* practical
* precise
* maintainable
* implementation-aware

Avoid dogma, overengineering, and unnecessary abstraction.
