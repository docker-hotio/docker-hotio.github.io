---
hide:
  - navigation
---

Pullio is a bash script that you execute with cron or a systemd timer (or any other way that you prefer), it then does a `docker-compose pull` for all the containers configured to have notifications or updates enabled. It then checks if there's an update available and takes action according to your configuration. As you might have already guessed it, this script relies on docker-compose to do the heavy lifting and thus is only compatible with docker-compose managed containers.

Features:

- Discord notifications (see below for preview)
- Detailed info about what has changed for images that follow the Opencontainers Annotation Keys
- Execute script before sending notification
- Execute script before updating container, after container is stopped
- Private registries
- With `--tag` you can use seperate configs for hourly "Update available" notifications and on a daily schedule actually apply the updates.

## Configuration

You configure the scripts behaviour by adding one or more of the following labels to your `docker-compose.yml` for every container you want..

```text
...
labels:
  - "org.hotio.pullio.notify=true"
  - "org.hotio.pullio.update=true"
  - "org.hotio.pullio.discord.webhook=https://discord.com/api/webhooks/..."
  - "org.hotio.pullio.script.notify=bash /notify-script.sh"
  - "org.hotio.pullio.script.update=bash /update-script.sh"
  - "org.hotio.pullio.registry.authfile=/authfile.txt"
```

If you need to provide credentials for a Private Registry, this file's content needs to be as shown below.

```text
{
  "registry": "ghcr.io",
  "username": "your_username",
  "password": "your_password"
}
```

## Notification preview

<img src="/img/pullio-preview.png" alt="sample-screen" width="400">