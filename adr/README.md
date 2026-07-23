# Architecture Decision Records

ADRs record significant cross-project decisions, the alternatives considered, and the
consequences accepted. They are numbered sequentially and use lowercase kebab-case file
names. New ADRs should start from the [ADR template](../templates/ADR.template.md).

## Accepted decisions

- [ADR 0001: Use Prettier for cross-project code formatting](0001-use-prettier.md) — establishes Prettier as the default formatter while leaving room to revisit Biome and oxfmt.
- [ADR 0002: Use the Commons Clause with the MIT License for source-available software](0002-use-commons-clause-with-mit.md) — establishes the source-available licensing model for MiKode software.

The decisions above are accepted. Any change to them should be documented in a new or
superseding ADR rather than rewriting their historical reasoning.

## Proposed decisions

- [ADR 0003: Use pnpm as the package manager](0003-use-pnpm.md) — proposes pnpm for consistent, strict, reproducible installs across projects.
- [ADR 0004: Support Node.js 22 and later](0004-support-node-22-and-later.md) — proposes Node.js 22.13 as the support floor with development on the active LTS line.
- [ADR 0005: Use a strict shared TypeScript configuration via @mikode/tsconfig](0005-use-strict-shared-typescript-configuration.md) — proposes strict compiler settings shared through an independent package.
- [ADR 0006: Use ESLint with a shared @mikode/code-quality configuration](0006-use-eslint-via-code-quality-package.md) — proposes type-aware linting, import hygiene, and React accessibility rules through an independent package.

Proposed decisions become accepted when confirmed; their related standards stay `Draft`
until then.
