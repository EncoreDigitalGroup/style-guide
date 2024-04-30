# GitHub Dependabot Guide

## Overview

This guide will help you understand how Encore Digital Group uses GitHub Dependabot to keep our project's dependencies up to date.
Previously, we would let Dependabot run every weekday starting at noon. This was great because it allowed us to keep our
dependencies up to date within about 24 hours of a new release. However, we found that this was causing a lot of noise
with merge conflicts in our `composer.json` and `package.json` files which required manual resolution.

In an effort to reduce the amount of noise with Automated Pull Requests (APRs), we have changed our Dependabot schedule to
run once a week on Wednesdays at noon. Why did we chose this time? Encore Digital Group is primarily a PHP and Laravel shop. Laravel
releases new versions every Tuesday. By running Dependabot on Wednesday, we are guaranteed to have an APR for latest minor and patch
versions of Laravel within 24 hours of release.

After an APR is opened by Dependabot, our CI Pipeline takes over. The CI Pipeline can vary from project to project, but in general
it performs the following steps:

1. APR is opened by Dependabot.
2. Codified style guide rules are applied to the APR.
3. The CI Pipeline runs the tests.
4. If the tests pass, static analysis is run.
5. If static analysis passes, the following checks occur:
    - Is this an APR and was it opened by Dependabot?
    - Does this APR update the dependency to the latest minor or patch version?

If all of the checks in the CI Pipeline pass, the APR is automatically merged. If any of the checks fail, a developer must review the APR.
One such example of steps 1-4 passing and step 5 failing is when a new major version of a dependency is released. In this case, the APR
doesn't break anything in the project, but due to the new major version of the dependency, a developer is assigned to review the APR and
ensure we are ready for the new major dependency version in the project.

## Our Basic Dependabot Configuration

```yaml
version: 2
updates:
  - package-ecosystem: "composer"
    directory: "/"
    schedule:
      interval: weekly
      day: wednesday
      time: "12:00"
      timezone: America/Chicago
    reviewers:
      - "EncoreDigitalGroup/dependency-management"
```

## Our APR Merge Checks

```yaml
name: Dependabot Auto-Merge
on:
  workflow_call:

permissions:
  pull-requests: write
  contents: write

jobs:
  Dependabot:
    runs-on: ubuntu-latest
    if: ${{ github.actor == 'dependabot[bot]' }}
    steps:

      - name: Dependabot Metadata
        id: metadata
        uses: dependabot/fetch-metadata@v1.6.0
        with:
          github-token: "${{ secrets.GITHUB_TOKEN }}"


      - name: Approve the PR
        run: gh pr review --approve "$PR_URL"
        env:
          PR_URL: ${{github.event.pull_request.html_url}}
          GITHUB_TOKEN: "${{ github.token }}"

      - name: Auto-merge Dependabot PRs for semver-minor updates
        if: ${{steps.metadata.outputs.update-type == 'version-update:semver-minor'}}
        run: gh pr merge --auto --squash "$PR_URL"
        env:
          PR_URL: ${{github.event.pull_request.html_url}}
          GITHUB_TOKEN: "${{ github.token }}"

      - name: Auto-merge Dependabot PRs for semver-patch updates
        if: ${{steps.metadata.outputs.update-type == 'version-update:semver-patch'}}
        run: gh pr merge --auto --squash "$PR_URL"
        env:
          PR_URL: ${{github.event.pull_request.html_url}}
          GITHUB_TOKEN: "${{ github.token }}"
```

This GitHub Workflow is open sourced and can be used in your project if you wish. To include it in your project, simply add the following
to the `jobs` section of your GitHub Workflow:

```yaml
AutoMerge:
 needs: Duster
 name: AutoMerge
 uses: EncoreDigitalGroup/.github/.github/workflows/dependabotAutoMerge.yml@v1
```