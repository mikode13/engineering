# Package management standard

- Status: Draft
- Last reviewed: 2026-07-24
- Related ADRs: [ADR 0003: Use pnpm as the package manager](../adr/0003-use-pnpm.md)

## Scope

This standard applies to all MiKode JavaScript and TypeScript repositories that install
npm-registry dependencies.

## Rules

Projects adopting this standard MUST:

1. Use pnpm for installing dependencies and running package scripts.
2. Pin the pnpm version in the `package.json` `packageManager` field.
3. Commit `pnpm-lock.yaml` and keep it in sync with `package.json`.
4. Use `pnpm install --frozen-lockfile` in CI so builds fail when the lockfile is out of
   date instead of silently resolving different versions.
5. Use pnpm commands in scripts, documentation, and contributor instructions.

Projects MUST NOT:

- Commit `package-lock.json` or `yarn.lock`.
- Rely on Corepack to provision pnpm. Corepack is not distributed with Node.js 25 and
  later; developers install pnpm with one of the
  [documented installation methods](https://pnpm.io/installation). Once installed, pnpm
  reads the `packageManager` field and can switch to the pinned version itself.

## Required configuration

`package.json` MUST contain a pinned pnpm version:

```json
{
  "packageManager": "pnpm@11.17.0"
}
```

The version is an exact version, not a range. Renovate-style tooling or a deliberate
manual update changes it; individual developers do not need matching global installs
because pnpm defers to the pinned version.

The CI install step is:

```sh
pnpm install --frozen-lockfile
```

## Exceptions

A project MAY use a different package manager only when an external platform requires it
(for example, a deployment target that only supports npm). The project MUST document the
exception and its reason in its README.

## Adoption

New projects start with `pnpm init` and the configuration above. Existing projects with
another lockfile migrate with `pnpm import`, which converts the existing lockfile, then
delete the old lockfile in the same change.

## References

- [ADR 0003: Use pnpm as the package manager](../adr/0003-use-pnpm.md)
- [pnpm installation](https://pnpm.io/installation)
- [pnpm CLI: install](https://pnpm.io/cli/install)
- [pnpm CLI: import](https://pnpm.io/cli/import)
- [npm `packageManager` field](https://nodejs.org/api/packages.html#packagemanager)
