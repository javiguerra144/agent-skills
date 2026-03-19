---
name: "documentation-generation"
description: "Use when generating, structuring, or improving technical documentation, including API docs, references, tutorials, ADRs, changelogs, OpenAPI specs, Mermaid diagrams, and larger documentation workflows."
---

# Documentation Generation

Use this skill for technical documentation work derived from the `wshobson/agents` `plugins/documentation-generation` plugin. It packages the upstream material as one installable skill with targeted references.

## Use This Skill When

- Writing or reorganizing product or engineering documentation
- Generating API reference docs or OpenAPI specifications
- Creating architecture decision records
- Producing changelogs or release notes
- Writing tutorials, walkthroughs, and onboarding docs
- Generating Mermaid diagrams
- Building a documentation plan or workflow for a larger doc set

## Default Approach

1. Identify whether the task is API documentation, reference docs, tutorials, ADRs, changelogs, OpenAPI generation, diagrams, or a larger documentation workflow.
2. Load only the matching reference files from `references/`.
3. Ground the documentation in the actual code, product behavior, and visible interfaces.
4. Prefer clear structure, factual language, and maintainable update paths.
5. When documenting systems or APIs, include assumptions, constraints, and example usage where helpful.

## Fast Rules

- Write for the actual audience: operators, developers, integrators, or end users.
- Prefer implementation-grounded documentation over aspirational claims.
- Keep examples concrete and consistent with the documented behavior.
- Separate conceptual overviews, reference material, and step-by-step tutorials.
- Keep diagrams aligned with the actual system boundaries and terminology.
- Treat changelogs and ADRs as historical artifacts: they should be precise, dated, and easy to scan.

## Reference Map

Load only what you need:

- `references/docs-architect.md` -> high-level documentation strategy, structure, and information architecture.
- `references/api-documenter.md` -> API-focused documentation patterns and endpoint-oriented documentation guidance.
- `references/reference-builder.md` -> reference documentation structure and completeness patterns.
- `references/tutorial-engineer.md` -> tutorial sequencing, onboarding flows, and task-based instructional writing.
- `references/mermaid-expert.md` -> Mermaid diagrams for architecture, flows, sequences, and process visualization.
- `references/architecture-decision-records.md` -> ADR structure, decision capture, alternatives, and rationale documentation.
- `references/changelog-automation.md` -> changelog generation, release-note structure, and change categorization.
- `references/openapi-spec-generation.md` -> OpenAPI spec authoring and API contract generation guidance.
- `references/doc-generate.md` -> large end-to-end documentation generation workflow and operating procedure.

## Suggested Routing

- If the task is broad docs architecture or a large doc refresh, load `references/docs-architect.md` and `references/doc-generate.md`.
- If the task is API-centric, load `references/api-documenter.md`; for machine-readable API contracts also load `references/openapi-spec-generation.md`.
- If the task is reference docs, load `references/reference-builder.md`.
- If the task is tutorial or onboarding content, load `references/tutorial-engineer.md`.
- If the task involves design rationale or architectural tradeoffs, load `references/architecture-decision-records.md`.
- If the task is release communication, load `references/changelog-automation.md`.
- If the task needs diagrams, load `references/mermaid-expert.md`.

## Notes

- The bundled references are adapted from the upstream plugin source and kept separate for progressive disclosure.
- This skill overlaps with narrower repo skills like `app-docs`; use the more focused skill when the task is a straightforward README or function-doc request, and use this bundle when documentation scope is broader or more specialized.
- Prefer the repository's existing terminology, structure, and examples over generic templates when they conflict.
