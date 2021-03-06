# auto-build-bicep
[![Test](https://github.com/dciborow/auto-build-bicep/workflows/Test/badge.svg)](https://github.com/dciborow/auto-build-bicep/actions?query=workflow%3ATest)
[![reviewdog](https://github.com/dciborow/auto-build-bicep/workflows/reviewdog/badge.svg)](https://github.com/dciborow/auto-build-bicep/actions?query=workflow%3Areviewdog)
[![depup](https://github.com/dciborow/auto-build-bicep/workflows/depup/badge.svg)](https://github.com/dciborow/auto-build-bicep/actions?query=workflow%3Adepup)
[![release](https://github.com/dciborow/auto-build-bicep/workflows/release/badge.svg)](https://github.com/dciborow/auto-build-bicep/actions?query=workflow%3Arelease)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/dciborow/auto-build-bicep?logo=github&sort=semver)](https://github.com/dciborow/auto-build-bicep/releases)
[![action-bumpr supported](https://img.shields.io/badge/bumpr-supported-ff69b4?logo=github&link=https://github.com/haya14busa/action-bumpr)](https://github.com/haya14busa/action-bumpr)

This repo contains a action to run [bicep](https://pypi.org/project/bicep).

## Input

```yaml
inputs:
  github_token:
    description: 'GITHUB_TOKEN'
    default: '${{ github.token }}'
  workdir:
    description: 'Working directory relative to the root directory.'
    default: '.'
```

## Usage

```yaml
name: Auto Build Bicep
on:
  push:
    branches-ignore:
      - master
    paths:
      - '**.bicep'
      - '!**azuredeploy.json'
jobs:
  main:
    name: Auto Build Bicep
    runs-on: ubuntu-latest
    steps:
      - uses: dciborow/auto-build-bicep@v1
```

## Development

### Release

#### [haya14busa/action-bumpr](https://github.com/haya14busa/action-bumpr)
You can bump version on merging Pull Requests with specific labels (bump:major,bump:minor,bump:patch).
Pushing tag manually by yourself also work.

#### [haya14busa/action-update-semver](https://github.com/haya14busa/action-update-semver)

This action updates major/minor release tags on a tag push. e.g. Update v1 and v1.2 tag when released v1.2.3.
ref: https://help.github.com/en/articles/about-actions#versioning-your-action

### Lint - reviewdog integration

This reviewdog action template itself is integrated with reviewdog to run lints
which is useful for Docker container based actions.

![reviewdog integration](https://user-images.githubusercontent.com/3797062/72735107-7fbb9600-3bde-11ea-8087-12af76e7ee6f.png)

Supported linters:

- [reviewdog/action-shellcheck](https://github.com/reviewdog/action-shellcheck)
- [reviewdog/action-hadolint](https://github.com/reviewdog/action-hadolint)
- [reviewdog/action-misspell](https://github.com/reviewdog/action-misspell)

### Dependencies Update Automation
This repository uses [reviewdog/action-depup](https://github.com/reviewdog/action-depup) to update
reviewdog version.
