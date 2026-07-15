# ADR 0001: Start with the platform contract before cloud provisioning

## Status

Accepted

## Context

Kliemt.One is intended to unify multiple existing and future legal technology tools, including JobRadar, KTS2.0, intake, legal research, and agent-built workflows. The platform must support fast prototyping while protecting confidentiality, data protection, maintainability, and review quality.

A possible first step would be to create Azure resources immediately and deploy from the repository. However, doing this before the repository contains architecture guidance, agent rules, and a minimal platform shape could encourage unreviewed prototype sprawl.

## Decision

The first step is to establish the platform contract in the repository: agent instructions, product vision, architecture baseline, and decision records. Azure resources should follow from infrastructure-as-code after the repository describes how the platform should be built and governed.

## Consequences

- Coding agents and humans receive immediate guidance before implementation begins.
- Early cloud work can be reviewed against written architecture principles.
- The project stays incremental and avoids premature commitment to unmanaged infrastructure.
- The next implementation step can be a minimal landing-page shell plus infrastructure-as-code for a restricted development environment.
