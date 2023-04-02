# Introduction

Log collector of flavor loki_s3 implementation

## Advanced Configuration

## Advanced

| Name                                | Description                                                                                                                                                                                         | Datatype           | Required |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------|----------|
| bucket_name                         | AWS S3 bucket name to distribute chunks. <br><br> Note: You can use AWS S3 module to create bucket and map the name using `${s3.<name-of-your-resource>.bucket_name}`                               | string             | yes      |
| loki.loki.values                    | Helm values as per the chart https://artifacthub.io/packages/helm/grafana/loki-distributed  Note: By default loki.structuredConfig.storage_config is configured to use minio storage backend | map< string, any > | no       |
| loki.minio.values                   | Helm values as per the chart https://artifacthub.io/packages/helm/bitnami/minio                                                                                                                     | map< string, any > | no       |
| loki.promtail.values                | Helm values as per the chart https://artifacthub.io/packages/helm/grafana/promtail  Note: By default, loki push endpoint will be configured automatically to send log entries to Loki        | map< string, any > | no       |
| loki.loki_canary.values             | Helm values as per the chart https://artifacthub.io/packages/helm/grafana/loki-canary  Note: By default, lokiAddress will be set with loki endpoint and serviceMonitor is enabled            | map< string, any > | no       |
| loki.loki_canary.enable_loki_canary | Whether to enable loki canary or not                                                                                                                                                                | boolean            | no       |

## Example usage
```json 
   "advanced": {
        "loki_s3": {
            "bucket_name": "loki",
            "loki": {
                "values": {}
            },
            "minio": {
                "values": {}
            },
            "promtail": {
                "values": {}
            },
        "loki_canary": {
            "enable_loki_canary": true,
            "values": {}
            }
        }
  }
```