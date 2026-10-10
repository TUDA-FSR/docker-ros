# Docker CI/CD for UAS Team

*Forked from https://github.com/ika-rwth-aachen/docker-ros*

This repo is used for Continuous Intergration / Continuous Development (CI/CD) by the UAS Team of FSR@TUDa. It was modified to comply with our GitLab environment and common workflow with UAS.

## Supported GitLab Runner Configuration

The GitLab workflow expects a runner service that uses [Docker in Docker with a Unix Socket on a Shared Volume](https://docs.gitlab.com/ci/docker/using_docker_build/#use-a-unix-socket-on-a-shared-volume-between-docker-in-docker-and-build-container). To use it with a different runner config, you need to overwrite the `DOCKER_HOST` variable. However, the default job's [DinD service](https://github.com/TUDA-FSR/docker-ros/blob/main/.gitlab-ci/docker-ros.yml#L107) might still interfer with other approaches.

## Registry Authentication

By default, the GitLab workflow logs in to the project's container registry (`CI_REGISTRY`) using the CI/CD job token. This is sufficient for pushing images to the project's own registry and for pulling base images from other private projects, as long as this project is added to the [CI/CD job token allowlist](https://docs.gitlab.com/ci/jobs/ci_job_token/#add-a-group-or-project-to-the-job-token-allowlist) of the project hosting the base image.

If credentials other than the job token are required, set `EXTRA_REGISTRY`, `EXTRA_REGISTRY_USER` and `EXTRA_REGISTRY_PASSWORD` in the project or group CI/CD settings:

| `EXTRA_REGISTRY` | Login to `CI_REGISTRY` with the job token | Login to `EXTRA_REGISTRY` with `EXTRA_REGISTRY_USER` and `EXTRA_REGISTRY_PASSWORD` |
| --- | --- | --- |
| empty (default) | yes | no |
| equal to `CI_REGISTRY` | no | yes |
| different from `CI_REGISTRY` | yes | yes |

If `EXTRA_REGISTRY` equals `CI_REGISTRY`, the extra credentials replace the job token for all registry access, including pushing. Hence, they must grant both read and write access to the project's registry.
