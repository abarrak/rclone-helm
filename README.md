# Rclone - Helm Chart
![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square)
![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)
[![CI (Lint)](https://github.com/abarrak/rclone-helm/actions/workflows/lint.yaml/badge.svg)](https://github.com/abarrak/rclone-helm/actions/workflows/lint.yaml)

This repository presents rclone helm chart to deploy in kubernetes.

## Features

- Job based deployment as `job` or `cronjob`.
- Supports setting up mutliple remotes (backends) in `rclone`.
- Customizable rclone command to run.
- Facilitates setting `rclone.conf` file through config map resource.
- Securely integrates credentials via external secrets operator.<br>
    (optioanl when implicit IAM auth methods are missing).
- Chart unit tests.

## Usage

```bash
helm repo add rclone https://abarrak.github.io/rclone-helm
helm install rclone-jobs rclone/rclone --version 1.0.0
```

## Chart Settings

You can customize both the job and rclone configuration in `values.yaml` file.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| backoffLimit | int | `3` |  |
| concurrencyPolicy | string | `"Forbid"` |  |
| destExternalSecret | string | `"destination-s3-rclone-creds-file"` |  |
| envVars[0].valueFrom.secretKeyRef.key | string | `"config"` |  |
| envVars[0].valueFrom.secretKeyRef.name | string | `"rclone-dest-sync-config"` |  |
| envVars[1].name | string | `"SOURCE_BUCKET"` |  |
| envVars[1].value | string | `""` |  |
| envVars[2].name | string | `"DEST_BUCKET"` |  |
| envVars[2].value | string | `""` |  |
| envVars[3].name | string | `"RCLONE_SOURCE_REMOTE_NAME"` |  |
| envVars[3].value | string | `""` |  |
| envVars[4].name | string | `"RCLONE_DEST_REMOTE_NAME"` |  |
| envVars[4].value | string | `""` |  |
| failedJobsHistoryLimit | int | `5` |  |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"rclone/rclone"` |  |
| image.tag | string | `"1.68"` |  |
| imagePullSecrets | list | `[]` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| rclone.command | string | `"rclone copy $RCLONE_SOURCE_REMOTE_NAME:\"$SOURCE_BUCKET/\" $RCLONE_DEST_REMOTE_NAME:\"$DEST_BUCKET/\" --config /opt/rclone.conf --log-level=DEBUG --retries=1 --fast-list --progress --ignore-checksum --metadata --metadata-include \"tier=STANDARD\"\n"` |  |
| rclone.config | string | `""` |  |
| resources.limits.cpu | string | `"700m"` |  |
| resources.limits.memory | string | `"1024Mi"` |  |
| resources.requests.cpu | string | `"100m"` |  |
| resources.requests.memory | string | `"256Mi"` |  |
| restartPolicy | string | `"OnFailure"` |  |
| schedule | string | `"0 10 * * *"` |  |
| securityContext | object | `{}` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automount | bool | `true` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| sourceExternalSecret | string | `"source-s3-rclone-creds-file"` |  |
| startingDeadlineSeconds | string | `""` |  |
| successfulJobsHistoryLimit | int | `5` |  |
| suspend | bool | `false` |  |
| timeZone | string | `""` |  |
| tolerations | list | `[]` |  |
| ttlSecondsAfterFinished | string | `"518400"` |  |
| volumeMounts[0].mountPath | string | `"/opt/rclone.conf"` |  |
| volumeMounts[0].name | string | `"rclone-conf"` |  |
| volumeMounts[0].readOnly | bool | `false` |  |
| volumeMounts[0].subPath | string | `"rclone.conf"` |  |
| volumeMounts[1].mountPath | string | `"/opt/source_provider_s3.creds"` |  |
| volumeMounts[1].name | string | `"source-creds"` |  |
| volumeMounts[1].readOnly | bool | `false` |  |
| volumeMounts[1].subPath | string | `"source_provider_s3.creds"` |  |
| volumeMounts[2].mountPath | string | `"/opt/dest_provider_s3.creds"` |  |
| volumeMounts[2].name | string | `"destination-creds"` |  |
| volumeMounts[2].readOnly | bool | `false` |  |
| volumeMounts[2].subPath | string | `"dest_provider_s3.creds"` |  |
| volumes[0].configMap.name | string | `"rclone"` |  |
| volumes[0].name | string | `"rclone-conf"` |  |
| volumes[1].name | string | `"source-creds"` |  |
| volumes[1].secret.secretName | string | `"rclone-source-sync-config"` |  |
| volumes[2].name | string | `"destination-creds"` |  |
| volumes[2].secret.secretName | string | `"rclone-dest-sync-config"` |  |
----------------------------------------------


## Support

In case this deployment option was helpful for you, and you liked it.

<a href="https://www.buymeacoffee.com/abarrak" target="_blank">
  <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 40px !important;width: 150px !important;" >
</a>

## License

MIT.
