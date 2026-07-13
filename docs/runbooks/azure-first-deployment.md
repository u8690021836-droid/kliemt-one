# Azure First Deployment Runbook

This runbook explains the recommended first manual Azure steps for bringing the static Kliemt.One landing page online while keeping production controlled.

## Branch strategy

Use `main` as the protected production branch. Coding agents and human contributors should work on short-lived feature branches such as `codex/create-kliemt-one-platform-architecture`, `codex/add-landing-page`, or `feature/jobradar-handoff`.

Recommended flow:

1. Keep `main` stable and protected.
2. Let agents create or update feature branches.
3. Open a pull request into `main`.
4. Require review from the legal tech / tech team before merge.
5. Deploy production only from `main`.
6. Deploy preview or development environments from feature branches when needed.

This means the agent may keep developing on branches, but production should be tied to `main` or a dedicated release branch, not to an agent branch.

## First Azure goal

For strict European data residency requirements, use **Azure Container Apps in an approved EU region** as the first hosting target. Static Web Apps is convenient, but Microsoft documents Static Web Apps as a global service whose static assets are globally distributed.

Container Apps is the better starting point for Kliemt.One because it lets the platform begin with an explicit deployment region, a container boundary, managed identity, Key Vault integration, private networking options, and a path toward APIs and worker services.

The current landing page is now container-ready through `Dockerfile` and `nginx.conf`.

## Azure Portal steps for the first landing page

1. Sign in to the Azure Portal.
2. Create or select a resource group in an approved EU region, for example `rg-kliemt-one-dev`.
3. Search for **Container App** in the Azure Portal marketplace.
4. Click **Create**.
5. Choose the subscription and resource group.
6. Set a container app name such as `ca-kliemt-one-dev`.
7. Create or select a Container Apps environment in an approved EU region, for example Germany West Central or West Europe depending on firm policy.
8. For the first deployment, use a container image built from this repository. GitHub Actions or Azure Container Registry can be added in the next step.
9. Enable ingress for the app.
10. Set target port to `8080`, matching the included Nginx container config.
11. Review and create the resource.

Do not put secrets into the container image or repository. Use managed identity and Key Vault when the platform starts connecting to protected services.

## GitHub repository settings

Before connecting production deployment, configure GitHub branch protection for `main`:

- require pull request before merge,
- require at least one reviewer,
- require status checks once CI exists,
- restrict direct pushes to `main`,
- keep secrets in GitHub Actions secrets or Azure Key Vault, never in source files.

## Recommended next repository step

After the Container App target is agreed, add infrastructure-as-code and a GitHub Actions workflow through a pull request. The workflow should build the container image, push it to an approved registry, and deploy only from the intended branch.

The next code step after that should be a small Azure Container Apps IaC deployment, not a large tool migration.
