# aboutme

Personal site at [www.yashasco.in](https://www.yashasco.in). Static HTML/CSS, no build step.

## Local preview

```bash
npx serve .
```

## Deploying

Same pattern as `wikis` / `svanaya` / `IntraScreener`: push to `main` →
`.github/workflows/deploy.yml` builds the image, pushes it to GHCR, and bumps
the tag in `home-infra` (`apps/aboutme/overlays/prod/kustomization.yaml`) —
ArgoCD picks up the change and rolls it out. No manual deploy step.

One-time setup this repo needs (not done by this workflow):
- `HOME_INFRA_PUSH_TOKEN` repo secret (a PAT with push access to `home-infra`).
- The home server's self-hosted Actions runner registered against this repo.
- A `ghcr-creds` image-pull secret in the `aboutme-prod` namespace on the cluster.
