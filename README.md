# renovate-semantic-commit-repro

> This repo contains the repro for this discussion: https://github.com/renovatebot/renovate/discussions/31973

## What it contains

A basic monorepo setup using Yarn workspaces, containing two packages:

- `pkg-a`
- `pkg-b`

### `pkg-a`

Contains the following dependencies:

- `lodash`, under `dependencies`, one version behind the latest.
- `ramda`, under `devDependencies`, one version behind the latest.

### `pkg-b`

Contains the following dependencies (basically the inverse of `pkg-a`):

- `lodash`, under `devDependencies`, one version behind the latest.
- `ramda`, under `dependencies`, one version behind the latest.

## The problem

When Renovate opens PRs bumping `lodash` and `ramda`, it uses different commit prefixes:

- `lodash` gets the `chore` prefix because it is listed under `devDependencies` in `pkg-b`.
- `ramda` gets the `fix` prefix because it is listed under `dependencies.` in `pkg-b`.

I'd imagine both of the PRs should have the `fix` prefix, since both these dependencies are listed under `dependencies` for at least 1 of the packages within the monorepo.
