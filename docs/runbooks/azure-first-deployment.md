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

## Create the Azure Container Registry first

Before the Container App can run the real Kliemt.One landing page, create a private Azure Container Registry for the image. Recommended portal values:

- Resource group: `Kliemt-one-RG`
- Registry name: `kliemtoneacr`
- Location: the same approved EU region as the Container Apps environment
- SKU: `Basic` for the first development deployment
- Admin user: disabled for the long-term target; use managed identity or a deployment identity instead

Portal steps:

1. Open a second Azure Portal tab.
2. Search for **Container Registry**.
3. Click **Create**.
4. Select `Kliemt-one-RG`.
5. Enter `kliemtoneacr` as the registry name. Registry names must be globally unique, lowercase, and contain only letters and numbers. If the name is taken, append a short suffix.
6. Select the same approved EU region as the Container Apps environment.
7. Select **Basic** SKU for now.
8. Review and create the registry.

After the registry exists, build and push this repository's container image to it. The preferred next repository step is to add GitHub Actions or infrastructure-as-code so this happens repeatably instead of through manual clicks.

## Azure Portal steps for the first landing page

1. Sign in to the Azure Portal.
2. Create or select a resource group in an approved EU region, for example `Kliemt-one-RG`.
3. Search for **Container App** in the Azure Portal marketplace.
4. Click **Create**.
5. Choose the subscription and resource group.
6. Set a container app name such as `kliemt-one-app`.
7. Create or select a Container Apps environment in an approved EU region, for example `kliemt-one-container-app-environment` in Germany West Central or West Europe depending on firm policy.
8. On the **Container** tab, leave **Use quickstart image** unchecked if you already have an Azure Container Registry image for this repository.
9. If you do not yet have a registry image, either stop here and create the registry/build pipeline first, or temporarily use the quickstart image only to validate the Azure environment. The quickstart image will not show the Kliemt.One landing page.
10. For the real Kliemt.One page, choose **Azure Container Registry**, select the approved registry, set the image to the Kliemt.One image, and set the tag, for example `latest` or a commit SHA.
11. Enable ingress for the app.
12. Set target port to `8080`, matching the included Nginx container config.
13. Review and create the resource.

## What to choose on the Container tab

Do **not** use the quickstart image for the real Kliemt.One landing page. The quickstart image is only a Microsoft sample container. It is useful for proving that the Container Apps environment works, but it does not deploy this repository.

Recommended options:

- **Best path**: create an Azure Container Registry, build this repository's `Dockerfile`, push the image, then select that image in the Container App wizard.
- **Acceptable temporary path**: use the quickstart image only as a disposable smoke test, then replace it with the real Kliemt.One image before sharing the URL.
- **Avoid**: treating the quickstart image as a real deployment or connecting production traffic to it.

Name guidance:

- Resource group: `Kliemt-one-RG` is acceptable.
- Container app: `kliemt-one-app` is acceptable.
- Container Apps environment: prefer `kliemt-one-container-app-environment`. If `kleimt-one-container-app-environment` was typed accidentally, consider fixing it now so all names use `kliemt`.

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
