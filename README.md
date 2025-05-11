# 35860

## Current behavior

Renovate creates a PR that recommends upgrading docutils to >=0.21.2,<0.22.

The issue with that recommendation is that this project supports Python >=3.8
and the minimum recommended docutils version 0.21.2 already requires
Python >=3.9.

The underlying issue seems to be that Renovate runs only once without a specific
Python version context, so it does not have a chance to verify whether the
recommended package version is supported on a particular Python version.

## Expected behavior

Renovate should run once for each Python version supported by the project that
is being scanned. That enables it to ignore package dependencies that are not
for that Python version, and it enables it to verify whether a desired
dependent package it is about to recommend, is even supported on that Python
version. The end result would be a PR with changes that have `python_version`
constraints if needed according to the supported Python versions.

If a particular recommended version of a dependent package cannot be used for
all Python versions supported by the project that is being scanned, then
it could be listed as a warning in the "Dependency Dashboard" issue.

## Link to the Renovate issue or Discussion

[Renovate discussion 35860](https://github.com/renovatebot/renovate/discussions/35860).

[Renovate PR #1859](https://github.com/zhmcclient/python-zhmcclient/pull/1859)
in the production repo where this first was observed.
