# Kliemt.One

Kliemt.One is the planned unified platform for Kliemt Arbeitsrecht's internal and client-facing legal technology tools. It is designed to become the common backbone for tools such as JobRadar, KTS2.0, intake/legal research assistants, document generators, restructuring workflows, and future agent-built modules.

## Why this repository exists

Today, many useful tools exist as separate products with different codebases, design languages, data flows, and deployment patterns. Kliemt.One should become the place where they can gradually converge:

- one visual and interaction language,
- one secure identity and authorization model,
- one documented engineering and review process,
- one deployment and environment strategy,
- one agent-friendly set of rules for prototyping and integration,
- one path from experiment to reviewed production capability.

## Current phase

This repository is in **foundation phase**. The immediate goal is not to migrate every tool. The immediate goal is to create a stable product and engineering contract so that humans and coding agents can safely extend the platform in small steps.

## Recommended next small step

Do **not** start by creating Azure resources first. Start by agreeing the platform contract and deployment shape in this repository, then provision the smallest Azure environment from infrastructure-as-code.

A practical first milestone is:

1. create a documented platform vision and architecture baseline,
2. add a minimal landing-page shell using the Kliemt.One design direction,
3. add infrastructure-as-code for a restricted Azure Container Apps development environment,
4. connect GitHub Actions deployment only after the first shell and review gates exist.

This keeps the project agent-native without letting prototypes bypass governance.

## Running the landing page locally

The current implementation is a dependency-free static landing page. From the repository root, run:

```bash
python3 -m http.server 4173
```

Then open `http://127.0.0.1:4173/`.

## Repository map

- `index.html` — first Kliemt.One landing-page shell.
- `styles.css` — visual design system for the first shell.
- `AGENTS.md` — standing instructions for coding agents working in this repository.
- `docs/vision.md` — product vision, target users, and incremental roadmap.
- `docs/platform/architecture.md` — initial platform architecture and integration principles.
- `docs/adr/` — architecture decision records.

## Operating model

Kliemt.One should support a controlled innovation loop:

1. A lawyer identifies a need in the platform.
2. The need is described to a coding agent connected to this repository.
3. The agent creates a small branch or prototype under repository rules.
4. GitHub checks and a restricted dev deployment validate the change.
5. The legal tech / tech team reviews security, data protection, maintainability, and fit.
6. Approved capabilities are merged and promoted for broader use.

## First architectural stance

Kliemt.One should begin as a modular platform shell deployed to Azure, with Azure Container Apps as the first hosting target for web modules and APIs. Shared capabilities such as identity, audit logging, document generation, search, and database access should be introduced deliberately as real integrations require them.
