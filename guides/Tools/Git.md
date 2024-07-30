---
title: Git Style Guide
---

# Git Style Guide

## Overview

This style guide expands on the [common style guide](./../common.md).

## Branch Naming

- Branch names should be written in `kebab-case`. For example, if you are working on a feature that allows users to
  upload images, the branch name should be `upload-images`.
- The exception to this rule is when you are generating branch names from Jira or another project management tool. In
  this case, the branch name should be the ticket number followed by a short description of the ticket. For example,
  `JIRA-1234-upload-images`.

## Commit Messages

- Git commit messages should be written in the present tense. For example, if you are adding a new feature, the commit
  message should be `Add new feature` instead of `Added new feature`.
- Commit messages should be concise and meaningful. There should be no need to write a novel in a commit message. If
  there is a need to write a novel, the changes should be broken up into smaller commits.
- If the project you're working in is broken into modules, the commit message should be prefixed with `[Module Name]`.
  For example, if you are working on the `Media Manager` module, the commit message should be `[Media Manager] Add new
  feature`.

## Version Tagging

- Encore Digital Group follows [semantic versioning](https://semver.org) when it comes to git tags. When tagging a
  release, the tag should be in the format of `vX.Y.Z`. For example, if you are tagging version 1.2.3, the tag should
  be `v1.2.3`.
- If you are tagging a release candidate any other pre-release version, the tag should be in the format of
  `vX.Y.Z-rcN`. For example, if you are tagging release candidate 1 for version 1.2.3, the tag should be `v1.2.3-rc1`.
- Encore Digital Group does not observe patch or minor version numbers in release candidate suffixes. If you are
  tagging another release candidate for version 1.2.3 after `v1.2.3-rc1`, the tag should be `v1.2.3-rc2` and
  not `v1.2.3-rc1.N`.