# Docker CI/CD for UAS Team

*Forked from https://github.com/ika-rwth-aachen/docker-ros*

This repo is used for Continuous Intergration / Continuous Development (CI/CD) by the UAS Team of FSR@TUDa. It was modified to comply with our GitLab environment and common workflow with UAS.

## Supported GitLab Runner Configuration

The GitLab workflow expects a runner service that uses [Docker in Docker with Unix Socket Binding](https://docs.gitlab.com/ci/docker/using_docker_build/#use-docker-socket-binding). To use it with a different runner config, you need to overwrite the `DOCKER_HOST` variable. However, the default's job [DinD service](https://github.com/TUDA-FSR/docker-ros/blob/main/.gitlab-ci/docker-ros.yml#L107) might still interfer with other approaches.
