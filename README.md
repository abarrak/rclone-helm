# Rclone - Helm Chart

This repository presents rclone helm chart to deploy in kubernetes,

## Features

- Job based deployment as `job` or `cronjob`.
- Supports setting up mutliple remotes (backends) in `rclone`.
- Customizable rclone command to run.
- Facilitates setting `rclone.conf` file through config map resource.
- Securely integrates credentials via external secrets as optional.
- Chart unit tests.

## Usage

```bash
helm repo add rclone https://abarrak.github.io/rclone-helm
helm install rclone-jobs rclone/rclone --version 1.0.0
```

## Chart Settings


## Support

If this deployment option for rclone helped and you liked it, you can send me coffee 😄

<a href="https://www.buymeacoffee.com/abarrak" target="_blank">
  <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 45px !important;width: 160px !important;" >
</a>

## License

MIT.
