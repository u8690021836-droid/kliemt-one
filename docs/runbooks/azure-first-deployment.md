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

For the current static landing page, the smallest useful Azure target is **Azure Static Web Apps**. It is simpler than Azure Container Apps for the current repository because there is no server process yet.

Use Azure Container Apps later when Kliemt.One has APIs, background jobs, PDF generation services, or tool-specific containers.

## Azure Portal steps for the first landing page

1. Sign in to the Azure Portal.
2. Create or select a resource group, for example `rg-kliemt-one-dev`.
3. Search for **Static Web App** in the Azure Portal marketplace.
4. Click **Create**.
5. Choose the subscription and resource group.
6. Set a name such as `kliemt-one-dev`.
7. Choose a nearby region supported by Azure Static Web Apps.
8. Under deployment details, choose **GitHub** as the source.
9. Authorize Azure to access the GitHub organization/repository if prompted.
10. Select the Kliemt.One repository.
11. Select the branch to deploy:
    - choose `main` for a controlled production-style deployment;
    - choose a temporary feature branch only for preview/dev experiments.
12. For build details, choose **Custom**.
13. Set the app location to `/`.
14. Leave the API location empty.
15. Leave the output location empty because the landing page is plain static HTML/CSS.
16. Review and create the resource.

Azure will create a GitHub Actions workflow in the repository. Review that workflow in a pull request before treating it as production deployment infrastructure.

## GitHub repository settings

Before connecting production deployment, configure GitHub branch protection for `main`:

- require pull request before merge,
- require at least one reviewer,
- require status checks once CI exists,
- restrict direct pushes to `main`,
- keep secrets in GitHub Actions secrets or Azure Key Vault, never in source files.

## Recommended next repository step

After the Static Web App is created, add the generated GitHub Actions workflow to the repository through a pull request and verify that deployments happen only from the intended branch.

The next code step after that should be a small deployment documentation update or a simple CI check, not a large tool migration.
