# ADR 0004: Support Node.js 22 and later

- Status: Proposed
- Date: 2026-07-24

## Context

MiKode libraries and applications need an explicit Node.js support policy. Without one,
each project guesses which runtime features are safe to use, and consumers cannot tell
which Node.js versions a published package supports.

At the time of this decision, the Node.js release schedule is:

- Node.js 20 reached end of life in April 2026.
- Node.js 22 is in maintenance LTS until April 30, 2027.
- Node.js 24 is the active LTS line, supported until April 30, 2028.
- Node.js 26 is the current line and is scheduled to become LTS in October 2026.

The toolchain also sets a floor: pnpm 11 requires Node.js 22.13 or later, and ESLint 10
requires 20.19, 22.13, or 24 and later.

## Decision

MiKode packages will support Node.js 22.13 and later within even-numbered (LTS) release
lines. Development and CI primarily use Node.js 24, the active LTS line.

Each project declares the supported range in `package.json` `engines` and pins the
development version in an `.nvmrc` file, as defined in the
[Node.js version standard](../standards/nodejs-version.md).

The minimum version is reviewed when a supported line reaches end of life or a new line
becomes LTS; raising it for published packages is a breaking change and follows the
project's versioning rules.

## Alternatives considered

### Minimum Node.js 24

Requiring the active LTS line would allow its newer APIs everywhere but would exclude
consumers still on Node.js 22, which receives security updates until April 2027. The
compatibility cost outweighs the feature gain while 22 remains supported.

### Minimum Node.js 20

Node.js 20 reached end of life in April 2026. Supporting an unmaintained runtime would
extend MiKode's support surface to versions that no longer receive security fixes.

### Tracking the current (odd or newest) release line

Odd-numbered lines never become LTS and are unsupported months after release. Building
against them would force consumers onto short-lived runtimes.

## Consequences

### Positive

- Libraries state a clear, verifiable support range that consumers can rely on.
- Development happens on the recommended, actively supported LTS line.
- Language and API features available in Node.js 22 can be used unconditionally.
- The policy has a built-in review trigger tied to the official release schedule.

### Negative

- Features introduced after Node.js 22 cannot be used in published packages until the
  floor is raised.
- The floor must be actively reviewed around each April/October schedule change; a
  stale floor silently extends support to end-of-life runtimes.
- Raising the floor later is a breaking change for consumers.

## Related standards

- [Node.js version standard](../standards/nodejs-version.md)

## References

Version-sensitive research performed on 2026-07-24.

- [Node.js releases and schedule](https://nodejs.org/en/about/previous-releases)
- [Node.js end-of-life dates](https://nodejs.org/en/about/eol)
- [Node.js release schedule repository](https://github.com/nodejs/Release)
