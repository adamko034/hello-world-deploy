# hello-world-deploy

Shared GitOps / Helm repository for:

- `helm/hello-world`
- `helm/good-night-world`

## Namespaces

| Env  | Namespace |
|------|-----------|
| DEV  | `dev`     |
| QA   | `qa`      |
| PROD | `prod`    |

## Desired versions (GitOps)

| File | Purpose |
|------|---------|
| `versions-qa.yaml` | Image tags for QA — updated by **release** jobs |
| `versions-prod.yaml` | Image tags for PROD — updated by **deploy-prod** |

```yaml
hello-world: "0.0.4"
good-night-world: "0.0.1"
```

DEV does **not** use these files (SNAPSHOT / build tag from CI).

QA/PROD Helm deploys set `image.tag` from the matching versions file.

## Layout

```text
versions-qa.yaml
versions-prod.yaml
helm/
  hello-world/
  good-night-world/
```
