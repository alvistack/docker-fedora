# Docker Image Packaging for Fedora

[![Travis](https://img.shields.io/travis/com/alvistack/docker-fedora.svg)](https://travis-ci.com/alvistack/docker-fedora)
[![GitHub release](https://img.shields.io/github/release/alvistack/docker-fedora.svg)](https://github.com/alvistack/docker-fedora/releases)
[![GitHub license](https://img.shields.io/github/license/alvistack/docker-fedora.svg)](https://github.com/alvistack/docker-fedora/blob/master/LICENSE)
[![Docker Pulls](https://img.shields.io/docker/pulls/alvistack/fedora.svg)](https://hub.docker.com/r/alvistack/fedora/)

Fedora Linux is a community-supported distribution derived from sources freely provided to the public by Red Hat for Red Hat Enterprise Linux (RHEL).

Learn more about Fedora: <https://www.fedora.org/>

## Supported Tags and Respective `Dockerfile` Links

  - [`32`, `latest`](https://github.com/alvistack/docker-fedora/blob/master/molecule/32/Dockerfile.j2)

## Overview

This Docker container makes it easy to get an instance of SSHD up and running with Fedora.

Based on [Official Fedora Docker Image](https://hub.docker.com/_/fedora/) with some minor hack:

  - Minimized `Dockerfile` for meta data definition
  - Provision by Ansible and Molecule Docker driver in single layer
  - Handle `ENTRYPOINT` with [catatonit](https://github.com/openSUSE/catatonit)
  - Handle `CMD` with SSHD

### Quick Start

Start SSHD:

    # Pull latest image
    docker pull alvistack/fedora
    
    # Run as detach
    docker run \
        -itd \
        --name fedora \
        --publish 2222:22 \
        alvistack/fedora

**Success**. SSHD is now available on port `2222`.

Because this container **DIDN'T** handle the generation of root password, so you should set it up manually with `pwgen` by:

    # Generate password with pwgen
    PASSWORD=$(docker exec -i fedora pwgen -cnyB1); echo $PASSWORD
    
    # Inject the generated password
    echo "root:$PASSWORD" | docker exec -i fedora chpasswd

Alternatively, you could inject your own SSH public key into container's authorized\_keys by:

    # Inject your own SSH public key
    (docker exec -i fedora sh -c "cat >> /root/.ssh/authorized_keys") < ~/.ssh/id_rsa.pub

Now you could SSH to it as normal:

    ssh root@localhost -p 2222

## Versioning

### `alvistack/fedora:latest`

The `latest` tag matches the most recent [GitHub Release](https://github.com/alvistack/docker-fedora/releases) of this repository. Thus using `alvistack/fedora:latest` or `alvistack/fedora` will ensure you are running the most up to date stable version of this image.

### `alvistack/fedora:<version>`

The version tags are rolling release rebuild by [Travis](https://travis-ci.com/alvistack/docker-fedora) in weekly basis. Thus using these tags will ensure you are running the latest packages provided by the base image project.

## License

  - Code released under [Apache License 2.0](LICENSE)
  - Docs released under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)

## Author Information

  - Wong Hoi Sing Edison
      - <https://twitter.com/hswong3i>
      - <https://github.com/hswong3i>
