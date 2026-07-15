# Kliemt.One Agent Instructions

Kliemt.One is intended to become the unified, agent-native platform for Kliemt Arbeitsrecht tools. Treat this repository as a long-lived product foundation, not a throwaway prototype.

## Working principles
- Make small, reviewable changes with clear documentation.
- Prefer boring, secure, auditable architecture over clever shortcuts.
- Keep German legal-sector confidentiality, professional secrecy, and GDPR expectations in mind for every feature.
- Do not add production secrets, client data, employee data, or credentials to the repository.
- Document important decisions as ADRs in `docs/adr/`.
- When adding a tool integration, define its ownership, data boundaries, authentication needs, and lifecycle before implementation.

## Product direction
- Kliemt.One should unify existing tools such as JobRadar, KTS2.0, intake/legal research, and future modules behind one coherent design, identity, and governance model.
- The platform should support agent-assisted prototyping while preserving review gates before firm-wide production use.
- New modules should be built as composable capabilities that can share approved identity, data, UI, and deployment foundations.

## Engineering guardrails
- Start with a thin platform shell, documentation, and deployment blueprint before migrating complex tools.
- Prefer Azure-native services where they reduce operational complexity.
- Every new app/module must include README-level usage notes, security assumptions, and test commands.
- Avoid creating broad abstractions until at least two real tools need them.

## Pull request expectations
- Summarize user-visible changes, architecture implications, and tests/checks performed.
- Call out any security, data protection, or deployment impacts.
