<div class="image-logo"><img src="/img/image-logos/bazarr.svg" alt="logo"></div>

[:octicons-mark-github-16: GitHub](https://github.com/hotio/bazarr){: .header-icons target=_blank rel="noopener noreferrer" }  
[:octicons-container-16: GitHub Registry](https://github.com/orgs/hotio/packages/container/package/bazarr){: .header-icons target=_blank rel="noopener noreferrer" }  
[:material-docker:{: style="transform: scale(1.3);" } Docker Hub](https://hub.docker.com/r/hotio/bazarr){: .header-icons target=_blank rel="noopener noreferrer" }  
[:octicons-link-16: Bazarr](https://github.com/morpheus65535/bazarr){: .header-icons target=_blank rel="noopener noreferrer" }  

--8<-- "includes/stats.md"

## Starting the container

!!! docker ""

    === "cli"

        ```shell
        docker run --rm \
            --name bazarr \
            -p 6767:6767 \
            -e PUID=1000 \
            -e PGID=1000 \
            -e UMASK=002 \
            -e TZ="Etc/UTC" \
            -v /<host_folder_config>:/config \
            hotio/bazarr
        ```

    === "compose"

        ```yaml
        version: "3.7"

        services:
          bazarr:
            container_name: bazarr
            image: hotio/bazarr
            ports:
              - "6767:6767"
            environment:
              - PUID=1000
              - PGID=1000
              - UMASK=002
              - TZ=Etc/UTC
            volumes:
              - /<host_folder_config>:/config
        ```

In most cases you'll need to add additional volumes, depending on your own personal preference, to get access to your files.

--8<-- "includes/tags.md"
