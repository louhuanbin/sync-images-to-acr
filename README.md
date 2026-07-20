## Sync deployment images to ACR

The GitHub Actions workflow at `.github/workflows/sync-images-to-acr.yml` mirrors the observability and MinIO images required by the AKS manifests into `pcncr3.azurecr.cn`.

Before manually running **Sync Images to ACR** from the Actions tab, add these repository secrets:

- `ACR_USERNAME`: ACR username, typically `pcncr3`
- `ACR_PASSWORD`: ACR admin password or a scoped repository-token password with push permission

The workflow mirrors these images:

- `clickhouse/clickhouse-server:25.12.5`
- `signoz/signoz-otel-collector:v0.144.5`
- `signoz/signoz:v0.132.2`
- `otel/opentelemetry-collector-contrib:0.118.0`
- `nginx:1.27-alpine`
- `minio/minio:RELEASE.2025-07-23T15-54-02Z`
- `minio/mc:RELEASE.2025-08-13T08-35-41Z`
- `quay.io/keycloak/keycloak:26.7.0`

```
  images=(
            "clickhouse/clickhouse-server:25.12.5|clickhouse/clickhouse-server:25.12.5"
            "signoz/signoz-otel-collector:v0.144.5|signoz/signoz-otel-collector:v0.144.5"
            "signoz/signoz:v0.132.2|signoz/signoz:v0.132.2"
            "otel/opentelemetry-collector-contrib:0.118.0|otel/opentelemetry-collector-contrib:0.118.0"
            "nginx:1.27-alpine|nginx:1.27-alpine"
            "minio/minio:RELEASE.2025-07-23T15-54-02Z|minio/minio:RELEASE.2025-07-23T15-54-02Z"
            "minio/mc:RELEASE.2025-08-13T08-35-41Z|minio/mc:RELEASE.2025-08-13T08-35-41Z"
            "quay.io/keycloak/keycloak:26.7.0|quay.io/keycloak/keycloak:26.7.0"
          )

```

Each entry uses `source_image|target_image`. If the `|target_image` part is omitted,
the workflow mirrors the image to the same repository path under ACR.