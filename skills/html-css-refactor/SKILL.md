---
name: "html-css-refactor"
description: "Use when refactoring or regenerating existing HTML into clean semantic markup or component-based UI, with output options such as HTML+CSS or React/Vue/Angular plus CSS or SASS, responsive improvements, CSS variables, and UI polish guided by the ui-design skill."
---

# HTML CSS Refactor

Use this skill when the user provides existing HTML and wants it rewritten into cleaner, more maintainable UI code.

This skill is for regeneration work, not only small edits. It should take messy markup, inline styles, repeated values, or weak layout structure and turn it into a cleaner implementation that preserves the content and intent while improving maintainability.

## Use This Skill When

- Refactoring pasted HTML into cleaner semantic structure
- Moving inline styles or `<style>` blocks into a dedicated CSS file
- Converting static HTML into React, Vue, or Angular component structure
- Letting the user choose between plain CSS and SASS output
- Replacing repeated hard-coded values with CSS custom properties
- Improving responsiveness across mobile, tablet, and desktop
- Cleaning up class names and reducing unnecessary wrapper elements
- Polishing visual hierarchy, spacing, typography, and layout without changing the core content
- Turning a rough HTML prototype into production-ready static UI or component code

## Do Not Use This Skill When

- The user only wants a tiny one-line HTML fix
- The codebase already requires a different styling system and the user does not want CSS or SASS
- The task is primarily JavaScript behavior rather than HTML/CSS structure
- The user explicitly wants a pixel-faithful copy of an existing stylesheet with no cleanup

## Default Workflow

1. Inspect the provided HTML, linked assets, scripts, and any existing CSS.
2. Determine the target output first. Let the user choose when possible:
   - `HTML + CSS`
   - `HTML + SASS`
   - `React + CSS`
   - `React + SASS`
   - `Vue + CSS`
   - `Vue + SASS`
   - `Angular + CSS`
   - `Angular + SASS`
3. If the user did not specify a target, infer it from the repo and request, or default to `HTML + CSS`.
4. Preserve the user-visible content, behavior hooks, and important attributes such as `id`, `name`, `for`, `aria-*`, `data-*`, and form semantics unless there is a clear reason to improve them.
5. Replace non-semantic wrappers with meaningful structure where possible: `header`, `main`, `section`, `article`, `nav`, `aside`, `footer`, `figure`, `button`, `label`, and proper heading levels.
6. Export presentation into CSS or SASS instead of inline styles or scattered per-element styling.
7. Create a token layer in `:root` using CSS custom properties before writing component rules.
8. Use those variables consistently for color, spacing, typography, radius, shadow, layout width, and motion.
9. Make the layout mobile-first and responsive using modern CSS such as Flexbox, Grid, `clamp()`, `minmax()`, and content-driven breakpoints.
10. Simplify the DOM where possible. Remove wrapper noise, duplicate declarations, and style repetition.
11. Keep selectors readable and maintainable. Prefer component-oriented classes over brittle tag chains.
12. Return the cleaned output in the chosen target format and styling format.

## Target-Specific Expectations

- `HTML + CSS` or `HTML + SASS`: keep the output semantic and file-oriented, with clean class structure and no framework assumptions.
- `React`: convert repeated UI regions into sensible components, keep JSX accessible, and preserve behavior hooks that matter to the app.
- `Vue`: use Single File Component structure when that matches the codebase, and keep template, script, and style organization consistent with the repo.
- `Angular`: produce component-oriented markup that respects Angular template syntax and class/style file separation when the project already uses it.
- `SASS`: use nesting sparingly, keep specificity controlled, and still rely on CSS variables for design tokens rather than replacing them with only SASS variables.

## Fast Rules

- Prefer semantic HTML over `div` soup.
- Keep structure, presentation, and behavior concerns separate.
- Do not repeat raw hex colors, spacing values, or font sizes throughout the stylesheet when a variable should exist.
- Start tokens with a small stable set instead of generating dozens of unused variables.
- Favor semantic tokens over purely visual names when possible, such as `--color-text`, `--color-surface`, and `--space-md`.
- Use fluid sizing where it improves readability, especially with `clamp()`.
- Design mobile-first, then enhance upward with media queries.
- Preserve accessibility while refactoring: focus styles, contrast, heading order, labels, landmarks, and touch targets.
- Keep class names consistent with the existing repo convention. If none exists, choose simple component-oriented names.
- Do not switch the target stack unless the user asked for it or the repo clearly requires it.
- Prefer CSS variables as the token system even when the styling output is SASS.

## CSS Variable Baseline

Unless the repo already defines tokens, start with a compact set like:

- Colors: background, surface, text, muted text, border, accent, accent contrast
- Typography: font family, font sizes, line heights, font weights
- Spacing: xs, sm, md, lg, xl
- Radius: sm, md, lg
- Shadow: subtle, elevated
- Layout: content width, gutter
- Motion: transition duration and easing

If the UI has repeated component-specific values, add component tokens only after the base tokens are in place.

## Responsive Expectations

- Use a mobile-first base layout.
- Let components wrap naturally before adding more breakpoints.
- Prefer Grid for 2D layout and Flexbox for linear alignment.
- Use `repeat(auto-fit, minmax(...))` or similar patterns for card grids and repeatable blocks.
- Use `clamp()` for major text and spacing values when fluid scaling improves the result.
- Add only the breakpoints the layout actually needs.

## Design Guidance Routing

This skill should reuse the repository's `ui-design` skill instead of duplicating visual design guidance.

Load these files only when needed:

- `skills/ui-design/SKILL.md` -> overall routing for UI design work
- `skills/ui-design/references/ui-designer.md` -> component and layout polish
- `skills/ui-design/references/responsive-design.md` -> responsive structure, fluid sizing, and breakpoint strategy
- `skills/ui-design/references/visual-design-foundations.md` -> typography, color, spacing, and hierarchy refinement
- `skills/ui-design/references/design-system-patterns.md` -> CSS variable architecture and token hierarchy

Use `skills/bem-styling/SKILL.md` only if the user explicitly asks for BEM or the class naming problem is the main focus.

## Output Checklist

Before finishing, confirm:

- The output format matches the user's chosen target stack
- HTML or template structure is cleaner and more semantic
- Styles are extracted into CSS or SASS
- Repeated raw values are replaced with CSS variables where it improves maintainability
- Layout works on small and large screens
- Visual hierarchy is clearer than the source
- Accessibility did not regress
- Unnecessary wrappers and redundant selectors were removed

## Notes

- Preserve the existing brand and product language when one already exists.
- If the source HTML is only a rough mockup, you may improve the visual design more aggressively, but keep the information architecture intact.
- If the project already has tokens or a stylesheet architecture, extend it instead of replacing it wholesale.
