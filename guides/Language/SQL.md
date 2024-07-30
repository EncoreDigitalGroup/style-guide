---
title: SQL
---

# SQL Language Style Guide

## Overview

This style guide expands on the [common style guide](./../common.md).

## SQL Keywords

SQL Keywords in queries should be written in `UPPER_CASE`.

## Table Naming

### Table/View Prefix

Table names should be prefixed with the name of the application or service that the table is associated with. For
example, if a module is named `OpenAccessManager`, the tables associated with that module should be prefixed
with `oam_`. This also applies when creating views.

### Plural Naming

Each table should be names as if it will house multiple records. For example, if a table is created to store users in
the `OpenAccessManager` module, the table should be named `oam_users`.

### View Suffix

If a view is created, it should be suffixed with `_view`. For example, if a view is created to display all users in the
`OpenAccessManager` module, the view should be named `oam_users_view`. In this case, you would just use the `oam_users`
table, but this is just an example.

## Column Naming

### Sequence

If a column is created to store the order of items in a list, such as when creating the ability to sort the line items
on an invoice, it should be named `sequence`. The `sequence` column should be an integer.

### `Timestamp` Columns

When creating `Timestamp` columns, they should be named in the past tense. For
example, `published_at`, `unpublished_at`, and `deleted_at`.
