# Kliemt.One Vision

## Product thesis

Kliemt.One should become the unified workspace for Kliemt Arbeitsrecht's legal technology tools: a single place where lawyers can find, use, request, and help evolve digital workflows.

The platform should feel like it was made *aus einem Guss*: coherent, trusted, modern, and tailored to employment-law work rather than a collection of unrelated tools.

## Example tools to converge

- **JobRadar**: search for suitable online job postings, select relevant postings, and generate PDFs for legal workflows such as Annahmeverzug contexts.
- **KTS2.0**: support restructuring projects, including Sozialplan calculations and project workflows.
- **Intake / legal research**: client intake, research assistance, Azure AI Search based chat, and knowledge retrieval.
- **Future modules**: document generation, termination offer workflows, project dashboards, calculators, and client-facing portals.

## Target users

- Lawyers who need reliable tools without switching contexts.
- Legal tech and knowledge teams who review, improve, and govern modules.
- IT/security teams who need predictable deployment, identity, and data boundaries.
- Coding agents that need precise repository rules to prototype safely.

## Guiding principles

1. **Unified, not monolithic**: tools should share platform foundations while remaining independently evolvable modules.
2. **Agent-native, review-gated**: coding agents should accelerate prototypes, but production release requires human review.
3. **Security by default**: identity, permissions, auditability, and data minimization are product features.
4. **Incremental migration**: existing tools should be integrated step-by-step when a real workflow needs them.
5. **Legal-workflow first**: technology choices should serve concrete employment-law processes.

## Incremental roadmap

### Phase 0 — Foundation

- Establish repository instructions, architecture documents, and ADRs.
- Define initial deployment direction and governance process.
- Build a minimal landing-page shell.

### Phase 1 — Platform shell

- Add authentication and role-aware navigation.
- Add module registry cards for tools such as JobRadar, KTS2.0, and intake.
- Add dev deployment pipeline with restricted Azure environment.

### Phase 2 — First real integration

- Pick one narrow workflow, such as a JobRadar handoff from a restructuring module.
- Define the data contract and permissions.
- Integrate through a small API rather than copying entire codebases into the platform.

### Phase 3 — Shared services

- Standardize audit logging, file storage, PDF generation, search, and database access.
- Create reusable design components and agent templates.
- Formalize promotion from prototype to production.
