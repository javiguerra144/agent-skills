---
name: "cicd-automation"
description: "Use when designing, debugging, or implementing CI/CD automation, including deployment pipelines, GitHub Actions, GitLab CI, secrets handling, Kubernetes delivery, Terraform-based infra changes, and DevOps troubleshooting."
---

# CI/CD Automation

Use this skill for CI/CD and DevOps work derived from the `wshobson/agents` `plugins/cicd-automation` plugin. It packages the upstream material as one installable skill with targeted references.

## Use This Skill When

- Designing a CI or CD pipeline
- Creating or reviewing GitHub Actions workflows
- Creating or reviewing GitLab CI pipelines
- Planning deployment gates, rollback, or progressive delivery
- Securing secrets and credentials in automation
- Troubleshooting failed builds, deploys, or runtime platform issues
- Working on Kubernetes delivery patterns
- Working on Terraform-backed infrastructure automation

## Default Approach

1. Identify whether the task is GitHub Actions, GitLab CI, deployment design, secrets, cloud architecture, Kubernetes, Terraform, or troubleshooting.
2. Load only the matching reference files from `references/`.
3. Prefer safe defaults: least privilege, explicit environments, rollback paths, and observable deploy steps.
4. Keep pipelines deterministic, cache-aware, and easy to debug.
5. When changing production delivery, include validation, failure handling, and rollback behavior.

## Fast Rules

- Separate build, test, security, and deploy concerns into clear stages.
- Treat secrets handling as a first-class requirement, not an afterthought.
- Prefer reusable workflows or templates when they reduce duplication without hiding critical behavior.
- Validate environment-specific behavior explicitly instead of relying on implicit branch logic.
- Add artifact retention, cache strategy, and failure visibility where they materially improve reliability.
- Design deployment steps so rollback is documented or automatable.

## Reference Map

Load only what you need:

- `references/deployment-pipeline-design.md` -> multi-stage pipeline design, approvals, deployment strategies, rollback, and progressive delivery.
- `references/github-actions-templates.md` -> GitHub Actions workflows for testing, building, containers, deployment, and security automation.
- `references/gitlab-ci-patterns.md` -> GitLab CI stages, runners, caching, artifacts, deployments, and GitOps-style patterns.
- `references/secrets-management.md` -> Vault, cloud secret managers, rotation, CI secret injection, and least-privilege guidance.
- `references/cloud-architect.md` -> cloud platform architecture guidance for resilient deployment environments.
- `references/devops-troubleshooter.md` -> incident-oriented troubleshooting for pipeline, infra, and deployment failures.
- `references/kubernetes-operations/k8s-manifest-generator.md` -> production-ready Kubernetes manifests for Deployments, Services, ConfigMaps, Secrets, PVCs, probes, and resource settings.
- `references/kubernetes-operations/helm-chart-scaffolding.md` -> Helm chart structure, templating, values organization, dependencies, and packaging workflows.
- `references/kubernetes-operations/gitops-workflow.md` -> ArgoCD or Flux GitOps workflows, declarative delivery, repo structure, sync strategy, and progressive delivery.
- `references/kubernetes-operations/k8s-security-policies.md` -> RBAC, NetworkPolicy, Pod Security Standards, and defense-in-depth cluster security guidance.
- `references/terraform-engineer.md` -> Terraform implementation workflow, module design, state handling, provider configuration, validation, and apply flow.
- `references/terraform-engineer/module-patterns.md` -> Terraform module interfaces, composition, and versioning.
- `references/terraform-engineer/state-management.md` -> remote state, locking, migrations, and workspace strategy.
- `references/terraform-engineer/providers.md` -> AWS, Azure, and GCP provider configuration and authentication.
- `references/terraform-engineer/testing.md` -> validation, linting, plan review, policy checks, and Terraform testing workflows.
- `references/terraform-engineer/best-practices.md` -> naming, security, DRY patterns, and maintainable Terraform conventions.
- `references/workflow-automate.md` -> large workflow automation playbook for building and evolving CI or CD workflows.

## Suggested Routing

- If the user wants a new CI workflow, load `references/workflow-automate.md` plus the platform-specific file.
- If the task is GitHub-specific, load `references/github-actions-templates.md`.
- If the task is GitLab-specific, load `references/gitlab-ci-patterns.md`.
- If the task is deployment architecture, load `references/deployment-pipeline-design.md`.
- If the task involves credentials, tokens, or secret rotation, load `references/secrets-management.md`.
- If the task involves raw manifests or workload specs, load `references/kubernetes-operations/k8s-manifest-generator.md`.
- If the task involves Helm packaging or chart templating, load `references/kubernetes-operations/helm-chart-scaffolding.md`.
- If the task involves GitOps, sync, reconciliation, or ArgoCD or Flux, load `references/kubernetes-operations/gitops-workflow.md`.
- If the task involves Kubernetes hardening, policy, RBAC, or network isolation, load `references/kubernetes-operations/k8s-security-policies.md`.
- If the task involves infra-as-code, load `references/terraform-engineer.md`.
- If the Terraform task is specifically about modules, state, providers, testing, or general best practices, also load the matching file under `references/terraform-engineer/`.
- If the user is debugging failures, load `references/devops-troubleshooter.md` and the platform-specific file involved.

## Notes

- The bundled references are adapted from the upstream plugin source and kept separate for progressive disclosure.
- The upstream `deployment-engineer.md` agent file is empty, so it is intentionally not bundled as a reference here.
- The Kubernetes reference has been replaced with the `kubernetes-operations` plugin from `wshobson/agents`, using targeted references for manifests, Helm, GitOps, and security.
- The Terraform reference has been replaced with the `terraform-engineer` skill from `Jeffallan/claude-skills`, including its bundled Terraform-specific references.
- Prefer the repository's existing CI platform and conventions over generic examples when they conflict.
