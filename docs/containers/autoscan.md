[![GitHub Source](https://img.shields.io/badge/github-source-ffb64c?style=flat-square&logo=github&logoColor=white&labelColor=757575)](https://github.com/hotio/autoscan)
[![GitHub Registry](https://img.shields.io/badge/github-registry-ffb64c?style=flat-square&logo=github&logoColor=white&labelColor=757575)](https://github.com/orgs/hotio/packages/container/package/autoscan)
[![Docker Pulls](https://img.shields.io/docker/pulls/hotio/autoscan?color=ffb64c&style=flat-square&label=pulls&logo=docker&logoColor=white&labelColor=757575)](https://hub.docker.com/r/hotio/autoscan)
[![Discord](https://img.shields.io/discord/610068305893523457?style=flat-square&color=ffb64c&label=discord&logo=discord&logoColor=white&labelColor=757575)](https://hotio.dev/discord)
[![Upstream](https://img.shields.io/badge/upstream-project-ffb64c?style=flat-square&labelColor=757575)](https://github.com/Cloudbox/autoscan)
[![Website](https://img.shields.io/badge/website-hotio.dev-ffb64c?style=flat-square&labelColor=757575)](https://hotio.dev/containers/autoscan)

## Starting the container

=== "cli"

    ```shell
    docker run --rm \
        --name autoscan \
        -p 3030:3030 \
        -e PUID=1000 \
        -e PGID=1000 \
        -e UMASK=002 \
        -e TZ="Etc/UTC" \
        -e PLEX_LOGIN="" \
        -e PLEX_PASSWORD="" \
        -v /<host_folder_config>:/config \
        hotio/autoscan
    ```

=== "compose"

    ```yaml
    version: "3.7"

    services:
      autoscan:
        container_name: autoscan
        image: hotio/autoscan
        ports:
          - "3030:3030"
        environment:
          - PUID=1000
          - PGID=1000
          - UMASK=002
          - TZ=Etc/UTC
          - PLEX_LOGIN
          - PLEX_PASSWORD
        volumes:
          - /<host_folder_config>:/config
    ```

If `PLEX_LOGIN` + `PLEX_PASSWORD` are not empty and the file `/config/app/plex.token` does not exist, an attempt is made to get a Plex token for Autoscan.

## Tags

--8<-- "tags/autoscan.md"

## Using a secure Plex connection

If you want to keep using secure connections within Plex, but don't wanna buy your own domain and keep the connection between Autoscan and Plex inside of their Docker network. Follow the below procedure.

Go to `https://plex.tv/pms/resources.xml?includeHttps=1&X-Plex-Token=xxxxxxxxxxxxxx` (replace `xxxxxxxxxxxxxx` with your token) and look for a url that looks like `https://10-1-0-100.xxxxxxxxxxxxx.plex.direct:32400`. That url can be used in your Autoscan plex target. You should however give the Plex container a static IP if you don't wanna do this every 5 minutes.
