# GitHub Actions Workflow for Building and Publishing Python Packages

Demo of building and publishing a Python package with Poetry and GitHub Actions.

Builds on [Publishing package distribution releases using GitHub Actions CI/CD workflows](https://packaging.python.org/en/latest/guides/publishing-package-distribution-releases-using-github-actions-ci-cd-workflows/)
and Poetry's own [poetry/.github/workflows/release.yaml](https://github.com/python-poetry/poetry/blob/main/.github/workflows/release.yaml).

The release pipeline consists of two GHA workflows -
[build.yaml](./.github/workflows/build.yaml) and [release.yaml](./.github/workflows/release.yaml).

The `build` workflow runs on every commit and pull request, running linters, tests, and other
checks to determine the releasability of the package.

The `release` workflow depends on the `build` and runs on a published
[GitHub release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository).
The `release` workflow is triggered by the
[`release.published` GitHub event](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows#release).

If the build is successful, the package can be released and
the workflow proceeds to the `release-to-github` and `release-to-pypi` steps.
