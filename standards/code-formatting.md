# Code formatting standard

- Status: Draft
- Last reviewed: 2026-07-24
- Related ADRs: [ADR 0001: Use Prettier for cross-project code formatting](../adr/0001-use-prettier.md)

This document describes the proposed standard. It becomes an active cross-project
requirement when ADR 0001 is accepted.

## Scope

This standard applies to MiKode software repositories that contain JavaScript,
TypeScript, JSX, TSX, JSON, YAML, Markdown, HTML, CSS, or other file types supported by
the selected Prettier version.

Generated files, vendored files, build output, and files produced by external tools are
not formatted as source code unless a project explicitly decides otherwise.

## Rules

Projects adopting this standard MUST:

1. Use Prettier as the formatter of record for supported source and documentation files.
2. Use the configuration in this document, either directly or through the independent
   `@mikode/code-style/prettier` package.
3. Keep the Prettier dependency, configuration, and lockfile under version control so
   local runs, editor integrations, and CI use reproducible behavior.
4. Provide a script or equivalent command for formatting files and a CI check that fails
   when tracked files are not formatted.
5. Configure ignored paths for generated, vendored, and otherwise excluded files instead
   of repeatedly formatting them by hand.
6. Treat formatting-only changes separately from behavior changes when practical, so
   reviewers can understand the change and adoption history.

Projects MUST NOT use a global Prettier installation or an undocumented editor-specific
configuration as the source of truth.

The standard does not prescribe architecture, linting, import ordering, naming, or other
code-quality rules. Those concerns belong in separate standards or project configuration.

## Required configuration

The following is a valid `.prettierrc.json` configuration:

```json
{
  "singleQuote": true,
  "semi": true,
  "trailingComma": "all",
  "arrowParens": "avoid",
  "quoteProps": "as-needed",
  "useTabs": true,
  "tabWidth": 2,
  "printWidth": 100,
  "endOfLine": "lf",
  "bracketSpacing": true,
  "bracketSameLine": false,
  "jsxSingleQuote": false,
  "proseWrap": "preserve",
  "objectWrap": "preserve",
  "singleAttributePerLine": false
}
```

These values have the following intent:

- Use single quotes in JavaScript and TypeScript, semicolons, trailing commas where
  supported, and unparenthesized single-argument arrow functions.
- Use tabs for indentation with a two-space tab width, a 100-character target print
  width, and LF line endings.
- Keep object wrapping and prose wrapping close to the author's intentional line breaks.
- Use spaces inside object braces, keep JSX brackets on their own line when multiline,
  and use double quotes for JSX attributes.

`printWidth` is a formatting target, not a hard maximum line length. Prettier may produce
longer lines when the syntax or readability requires it. The `objectWrap` option requires
a Prettier version that supports it; projects on an older version MUST document an
exception or use a compatible shared configuration.

Typical project scripts are:

```json
{
  "scripts": {
    "format": "prettier . --write",
    "format:check": "prettier . --check"
  }
}
```

Projects should invoke the locally installed formatter through their package manager. For
pnpm projects, the equivalent commands are:

```sh
pnpm exec prettier . --write
pnpm exec prettier . --check
```

The `format` command is for local development. The `format:check` command is the CI gate.

## Exceptions

A project MAY exclude a path when formatting it would alter generated output, third-party
content, or a format that Prettier cannot safely parse. The exclusion MUST be explicit in
`.prettierignore`, an override, or an equivalent project configuration, and the project
SHOULD explain the reason near the exception.

A project MAY change an option only when the default causes a documented compatibility or
readability problem. The project MUST record the deviation in its own documentation and
explain why the shared value is unsuitable. A cross-project change to these values requires
a new or updated ADR.

## Adoption

New projects should adopt the shared configuration before their first substantial feature.
Existing projects should adopt it in a dedicated formatting change, then add the CI check
before subsequent feature work.

When `@mikode/code-style/prettier` becomes available, projects should consume that package
rather than copying its implementation into this repository. This repository may retain
the documented option values so the policy remains understandable without reading package
source code.

## References

- [ADR 0001: Use Prettier for cross-project code formatting](../adr/0001-use-prettier.md)
- [Prettier options](https://prettier.io/docs/options.html)
- [Prettier configuration files](https://prettier.io/docs/configuration)
- [Prettier CLI](https://prettier.io/docs/cli)
