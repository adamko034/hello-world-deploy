# hello-world-deploy

Shared GitOps / Helm repository for microservices:

- `helm/hello-world`
- `helm/good-night-world`

Both apps deploy into the **same namespaces**:

| Env  | Namespace |
|------|-----------|
| DEV  | `dev`     |
| QA   | `qa`      |
| PROD | `prod`    |

## Layout

```text
helm/
  hello-world/
  good-night-world/
```

## Example

```bash
# DEV — hello-world
helm upgrade --install hello-world ./helm/hello-world \
  -n dev -f ./helm/hello-world/values-dev.yaml \
  --set image.repository=adamko034/hello-world \
  --set image.tag=<tag> \
  --create-namespace

# DEV — good-night-world
helm upgrade --install good-night-world ./helm/good-night-world \
  -n dev -f ./helm/good-night-world/values-dev.yaml \
  --set image.repository=adamko034/good-night-world \
  --set image.tag=<tag> \
  --create-namespace
```
