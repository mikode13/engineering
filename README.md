# MiKode Engineering

MiKode Engineering is the source of truth for cross-project engineering decisions,
standards, reusable documentation templates, and shared development practices.

It documents decisions and policies; it does not contain the production implementation of
MiKode libraries or applications. Reusable tooling belongs in its own package repository.

## Who should use this repository

MiKode maintainers, contributors, and project teams should use these documents when they
start a project, make a cross-project technical decision, or need to apply an existing
standard consistently.

## Documents

### Architecture Decision Records

ADRs preserve the reasoning behind significant decisions. They are historical records and
should not be rewritten to hide the trade-offs of an earlier decision.

See the [ADR index](adr/README.md).

### Standards

Standards describe the current or proposed rules for MiKode projects. A standard is only
active when its status says `Active`; proposed decisions and draft standards are not yet
mandatory.

See the [standards index](standards/README.md).

### Templates

Templates provide reusable starting files with explicit placeholders. A copied template
must be completed and validated in the target repository before it becomes effective.

See the [templates index](templates/README.md).

## Current work

The repository currently contains two proposed decisions and two draft standards:

- [ADR 0001: Use Prettier for cross-project code formatting](adr/0001-use-prettier.md)
- [ADR 0002: Use the Commons Clause with the MIT License for source-available software](adr/0002-use-commons-clause-with-mit.md)
- [Code formatting standard](standards/code-formatting.md)
- [Licensing standard](standards/licensing.md)

There are currently no active cross-project standards. The documents above become active
only after their related decisions are accepted.

## Documenting a new decision

Before adding a decision, confirm that it affects more than one MiKode project. Describe
the problem and constraints, research realistic alternatives, and record the proposed
decision in an ADR. Once the decision is confirmed, mark the ADR `Accepted`, update the
related standard, add or update a template when needed, and update the indexes.

Use relative links for documents in this repository and authoritative links for external
facts. Keep historical reasoning in ADRs and active rules in standards.
