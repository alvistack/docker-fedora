# Docker Image Packaging for Fedora

## 32-XalvistackY - TBC

### Major Changes

  - Add Node.js 15 support
  - Remove Node.js 14 support

## 32-4alvistack3 - 2020-10-14

### Major Changes

  - Refine Molecule matrix

## 32-4alvistack1 - 2020-09-07

  - Fedora 32 based
  - Minimized `Dockerfile` for meta data definition
  - Provision by Ansible and Molecule Docker driver in single layer
  - Handle `ENTRYPOINT` with [catatonit](https://github.com/openSUSE/catatonit)
  - Handle `CMD` with SSHD
