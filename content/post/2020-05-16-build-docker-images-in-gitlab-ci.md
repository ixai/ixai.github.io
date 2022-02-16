---
title: Build Docker images in GitLab CI
date: 2020-05-16
slug: build-docker-images-in-gitlab-ci
---

When implementing GitLab CI to build docker images, there were a few steps that weren't immediately obvious from [the documentation](https://gitlab.com/help/ci/quick_start/README.md).

First, you need to add Docker as a service.

```yaml
services:
  - docker:19.03.8-dind
```

Second, you need to install the docker CLI. For debian-based systems, that's `docker.io`, not `docker`.

```yaml
before-script:
  - apt-get update
  - apt-get install docker.io -yqq
```

Third, you need to point the docker CLI to talk to the Docker service.

```yaml
variables:
  DOCKER_HOST: tcp://docker:2375/
```
