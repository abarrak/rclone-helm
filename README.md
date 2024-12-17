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

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| backoffLimit | int | `3` |  |
| concurrencyPolicy | string | `"Forbid"` |  |
| enableExternalSecrets | bool | `false` | |
| enablePlainSecrets | bool | `false` | |
| envVars[0].name | string | `"RCLONE_CONFIG_FILE"` |  |
| envVars[0].value | string | `"/opt/rclone.conf"` |  |
| envVars[1].name | string | `"REMOTE_A_NAME"` |  |
| envVars[1].value | string | `""` |  |
| envVars[2].name | string | `"REMOTE_B_NAME"` |  |
| envVars[2].value | string | `""` |  |
| envVars[3].name | string | `"REMOTE_A_BUCKET"` |  |
| envVars[3].value | string | `""` |  |
| envVars[4].name | string | `"REMOTE_B_BUCKET"` |  |
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
| rclone.command | string | `"rclone copy $REMOTE_A_NAME:\"$REMOTE_A_BUCKET/\" $REMOTE_B_NAME:\"$REMOTE_A_BUCKET/\" --config $RCLONE_CONFIG_FILE --log-level=DEBUG --retries=1 --fast-list --progress --ignore-checksum --metadata --metadata-include \"tier=STANDARD\"\n"` |  |
| rclone.config | string | `""` |  |
| remoteBackendsExternalSecrets | list | `[]` |  |
| remoteBackendsSecrets | list | `[]` |  |
| resources.limits.cpu | string | `"500m"` |  |
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
| volumes[0].configMap.name | string | `"rclone"` |  |
| volumes[0].name | string | `"rclone-conf"` |  |
----------------------------------------------

## Support

In case this deployment option was helpful for you, and you liked it.

<a href="https://www.buymeacoffee.com/abarrak" target="_blank">
  <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 40px !important;width: 150px !important;" >
</a>

## License

MIT.
