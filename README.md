# Docker Image Packaging for Fedora

<a href="https://alvistack.com" title="AlviStack" target="_blank"><img src="/alvistack.svg" height="75" alt="AlviStack"></a>

[![GitLab pipeline status](https://img.shields.io/gitlab/pipeline/alvistack/docker-fedora/master)](https://gitlab.com/alvistack/docker-fedora/-/pipelines)
[![GitHub tag](https://img.shields.io/github/tag/alvistack/docker-fedora.svg)](https://github.com/alvistack/docker-fedora/tags)
[![GitHub license](https://img.shields.io/github/license/alvistack/docker-fedora.svg)](https://github.com/alvistack/docker-fedora/blob/master/LICENSE)
[![Docker Pulls](https://img.shields.io/docker/pulls/alvistack/fedora-38.svg)](https://hub.docker.com/r/alvistack/fedora-38)

Fedora is a Linux distribution developed by the community-supported Fedora Project which is sponsored primarily by Red Hat, a subsidiary of IBM, with additional support from other companies. Fedora contains software distributed under various free and open-source licenses and aims to be on the leading edge of free technologies. Fedora is the upstream source of the commercial Red Hat Enterprise Linux distribution, and subsequently CentOS as well.

Learn more about Fedora: <https://getfedora.org/>

## Supported Tags and Respective Packer Template Links

-   [`alvistack/fedora-rawhide`](https://hub.docker.com/r/alvistack/fedora-rawhide)
    -   [`packer/docker-rawhide/packer.json`](https://github.com/alvistack/docker-fedora/blob/master/packer/docker-rawhide/packer.json)
-   [`alvistack/fedora-38`](https://hub.docker.com/r/alvistack/fedora-38)
    -   [`packer/docker-38/packer.json`](https://github.com/alvistack/docker-fedora/blob/master/packer/docker-38/packer.json)
-   [`alvistack/fedora-37`](https://hub.docker.com/r/alvistack/fedora-37)
    -   [`packer/docker-37/packer.json`](https://github.com/alvistack/docker-fedora/blob/master/packer/docker-37/packer.json)
-   [`alvistack/fedora-36`](https://hub.docker.com/r/alvistack/fedora-36)
    -   [`packer/docker-36/packer.json`](https://github.com/alvistack/docker-fedora/blob/master/packer/docker-36/packer.json)

## Overview

This Docker container makes it easy to get an instance of SSHD up and running with Fedora.

Based on [Official Fedora Docker Image](https://hub.docker.com/_/fedora/) with some minor hack:

-   Packaging by Packer Docker builder and Ansible provisioner in single layer
-   Handle `ENTRYPOINT` with [catatonit](https://github.com/openSUSE/catatonit)
-   Handle `CMD` with SSHD

### Quick Start

Start SSHD:

    # Pull latest image
    docker pull alvistack/fedora-38

    # Run as detach
    docker run \
        -itd \
        --name fedora \
        --publish 2222:22 \
        alvistack/fedora-38

**Success**. SSHD is now available on port `2222`.

Because this container **DIDN'T** handle the generation of root password, so you should set it up manually with `pwgen` by:

    # Generate password with pwgen
    PASSWORD=$(docker exec -i fedora pwgen -cnyB1); echo $PASSWORD

    # Inject the generated password
    echo "root:$PASSWORD" | docker exec -i fedora chpasswd

Alternatively, you could inject your own SSH public key into container's authorized_keys by:

    # Inject your own SSH public key
    (docker exec -i fedora sh -c "cat >> /root/.ssh/authorized_keys") < ~/.ssh/id_rsa.pub

Now you could SSH to it as normal:

    ssh root@localhost -p 2222

## Versioning

### `YYYYMMDD.Y.Z`

Release tags could be find from [GitHub Release](https://github.com/alvistack/docker-fedora/tags) of this repository. Thus using these tags will ensure you are running the most up to date stable version of this image.

### `YYYYMMDD.0.0`

Version tags ended with `.0.0` are rolling release rebuild by [GitLab pipeline](https://gitlab.com/alvistack/docker-fedora/-/pipelines) in weekly basis. Thus using these tags will ensure you are running the latest packages provided by the base image project.

## License

-   Code released under [Apache License 2.0](LICENSE)
-   Docs released under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)

## Author Information

-   Wong Hoi Sing Edison
    -   <https://twitter.com/hswong3i>
    -   <https://github.com/hswong3i>
