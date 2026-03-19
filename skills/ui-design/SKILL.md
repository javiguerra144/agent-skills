---
name: "ui-design"
description: "Use when designing or reviewing UI and UX systems, including design systems, accessibility, responsive layouts, web components, mobile patterns, interaction design, visual foundations, and UI review or setup workflows."
---

# UI Design

Use this skill for UI and UX design work derived from the `wshobson/agents` `plugins/ui-design` plugin. It packages the upstream material as one installable skill with targeted references.

## Use This Skill When

- Designing or reviewing UI components and layouts
- Building or evolving a design system
- Auditing accessibility and WCAG compliance
- Creating responsive layouts across breakpoints and container sizes
- Designing web components, React/Vue/Svelte UI, or React Native screens
- Applying iOS or Android mobile design patterns
- Improving motion, interaction, and visual hierarchy
- Running a UI review, accessibility audit, or design system setup workflow

## Default Approach

1. Identify whether the task is design systems, accessibility, responsive layout, web UI, mobile UI, interaction design, or visual foundations.
2. Load only the matching reference files from `references/`.
3. Preserve the existing product language and design system where one already exists.
4. Balance aesthetics, usability, accessibility, and implementation realism.
5. When suggesting UI changes, make the rationale explicit: usability, consistency, performance, accessibility, or maintainability.

## Fast Rules

- Prefer clear hierarchy, spacing, and states over ornamental complexity.
- Treat accessibility as a baseline requirement, not a follow-up task.
- Keep interactions intentional and support keyboard and assistive-tech use.
- Use responsive patterns that adapt structurally, not just by shrinking.
- Make design tokens and component contracts explicit when scaling a system.
- Match the platform: web, iOS, Android, and React Native have different expectations.

## Reference Map

Load only what you need:

- `references/ui-designer.md` -> general UI design guidance, layout improvement, and component-level design thinking.
- `references/design-system-architect.md` -> design tokens, theming, component libraries, and design-system architecture.
- `references/accessibility-expert.md` -> accessibility analysis, WCAG compliance, and remediation strategy.
- `references/design-system-patterns.md` -> token systems, component architecture, and scalable system patterns.
- `references/accessibility-compliance.md` -> accessibility compliance details, inclusive design, and audit criteria.
- `references/responsive-design.md` -> responsive layout systems, breakpoints, fluid design, and container-query thinking.
- `references/web-component-design.md` -> web component patterns, framework component design, and CSS-in-JS or styling strategy.
- `references/interaction-design.md` -> motion, transitions, microinteractions, and user-flow refinement.
- `references/visual-design-foundations.md` -> typography, color, spacing, visual hierarchy, and iconography.
- `references/mobile-ios-design.md` -> iOS-specific design patterns and platform conventions.
- `references/mobile-android-design.md` -> Android and Material-style design patterns.
- `references/react-native-design.md` -> React Native design and cross-platform mobile UI guidance.
- `references/design-review.md` -> workflow for reviewing an existing UI and identifying issues or improvements.
- `references/create-component.md` -> guided component creation workflow with proper design and implementation patterns.
- `references/accessibility-audit.md` -> structured accessibility audit workflow.
- `references/design-system-setup.md` -> workflow for initializing a design system.

## Suggested Routing

- If the task is broad UI review, load `references/ui-designer.md` and `references/design-review.md`.
- If the task is about accessibility, load `references/accessibility-expert.md`, then `references/accessibility-compliance.md`, and use `references/accessibility-audit.md` for an audit workflow.
- If the task is about design systems, load `references/design-system-architect.md`, `references/design-system-patterns.md`, and `references/design-system-setup.md`.
- If the task is responsive or web-focused, load `references/responsive-design.md` and `references/web-component-design.md`.
- If the task is motion or interaction-focused, load `references/interaction-design.md`.
- If the task is visual polish, load `references/visual-design-foundations.md`.
- If the task is mobile-specific, load the matching iOS, Android, or React Native reference.
- If the user wants a new component, load `references/create-component.md` and the most relevant platform-specific file.

## Notes

- The bundled references are adapted from the upstream plugin source and kept separate for progressive disclosure.
- This skill overlaps with narrower repo skills like `frontend-developer` and `bem-styling`; use this bundle when the task is design-heavy or spans multiple UI concerns.
- Prefer the repository's existing design language and implementation constraints over generic examples when they conflict.
