# GitHub Actions Workflow for Building and Publishing Python Packages

Demo of building and publishing a Python package
with [Poetry](https://python-poetry.org/)
and [GitHub Actions](https://github.com/features/actions).

Builds on [Publishing package distribution releases using GitHub Actions CI/CD workflows](https://packaging.python.org/en/latest/guides/publishing-package-distribution-releases-using-github-actions-ci-cd-workflows/)
and Poetry's own [poetry/.github/workflows/release.yaml](https://github.com/python-poetry/poetry/blob/main/.github/workflows/release.yaml).

The release pipeline consists of two GHA workflows -
[`build.yaml`](./.github/workflows/build.yaml) and [`release.yaml`](./.github/workflows/release.yaml).

The `build` workflow runs on every commit and pull request, running linters, tests, and other
checks to determine the releasability of the package.

The `release` workflow depends on the `build` and runs on a published
[GitHub release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository).
The `release` workflow is triggered by the
[`release.published` GitHub event](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows#release).

If the build is successful, the workflow proceeds to the `release-to-github` and `release-to-pypi` steps.

## Publishing a new Package Release

1. Bump the package version in the [`pyproject.toml`](pyproject.toml).
   Commit and push the change to main.

2. Create a new GitHub release by going to Releases -> Draft a new release.

   Set the release title and release tag to the same package version as in `pyproject.toml`.
   The release pipeline will compare the package version from the `pyproject.toml`
   and GitHub release and fail the build if the versions don't match.
   It guards against releasing a package with an incorrect version,
   e.g., if the version wasn't updated in `pyproject.toml`.

3. The release pipeline will upload the package distribution to the GitHub release and Python package index.
