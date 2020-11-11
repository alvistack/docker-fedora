# Docker Image Packaging for Fedora

## 33-XalvistackY - TBC

### Major Changes

  - Support Fedora 33
  - Remove Fedora 32 support
  - Revamp with Packer

## 32-4alvistack3 - 2020-10-14

### Major Changes

  - Refine Molecule matrix

## 32-4alvistack1 - 2020-09-07

  - Fedora 32 based
  - Minimized `Dockerfile` for meta data definition
  - Provision by Ansible and Molecule Docker driver in single layer
  - Handle `ENTRYPOINT` with [catatonit](https://github.com/openSUSE/catatonit)
  - Handle `CMD` with SSHD
