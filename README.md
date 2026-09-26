# hello-world-deploy

GitOps / deploy repository for the **hello-world** microservice.

Holds the Helm chart and environment values. Application code and CI live in the app repo; this repo defines **what version runs where**.

## Layout

```text
helm/hello-world/          # Helm chart
  Chart.yaml
  values.yaml              # defaults
  values-dev.yaml          # DEV (SNAPSHOT / build tags)
  values-qa.yaml           # QA (released tags)
  values-prod.yaml         # PROD (released tags)
  templates/
```

## Usage

Jenkins (or later Argo CD) checks out this repo and runs:

```bash
helm upgrade --install hello-world ./helm/hello-world \
  -n hello-world-qa \
  -f ./helm/hello-world/values-qa.yaml \
  --set image.repository=adamko034/hello-world \
  --set image.tag=<version>
```

Promote by changing `image.tag` in the env values file (PR) and/or deploying via Jenkins with an explicit tag.
