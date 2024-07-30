---
title: PHP
---

# PHP Language Style Guide

## Overview

This style guide expands on the [common style guide](./../common.md).

## Naming

### Affirmative Naming

Always name identifiers in the affirmative. If you are setting a `bool` property that determines if redis should be used
for a given class, method, or function, name it `$useRedis` instead of `$dontUseRedis`. The exception to this is if you
are writing helper methods. It is much easier to determine the outcome of an `if` statement when the condition
is `Http::wasSuccessful()` or `Http::wasNotSuccessful()` rather than using a negative modifier.

### Concise Naming

Any identifier should be named as meaningful and concise as possible. If you are naming a parameter that accepts a
duration, instead of naming that parameter `$duration`, name it `$durationInSeconds` or whatever unit of time is
appropriate for that measurement.

### `DateTime` Properties

When creating `DateTime` properties, they should be named in the past tense. For
example, `publishedAt`, `unpublishedAt`, and `deletedAt`

## Properties

### Exception to `camelCase` Property Naming Rule

When writing Laravel Application and Package code, properties are created via the `$fillable` or `$gaurded` model
properties. The Laravel convention dictates that these properties should be `snake_case`.

### Private Properties

Properties should never be `private`. Only use `public` or `protected`. If you must treat a property as `private`, set
it as `protected` and do not create the associated getter or setter methods.
