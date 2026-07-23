# Templates

Templates are reusable starting files for MiKode projects. Replace every explicit
placeholder, verify the result, and copy the completed file into the target repository.

## Available templates

- [LICENSE.template](LICENSE.template) — MIT License text with the Commons Clause License Condition v1.0.

The license template is not legal advice and is not effective for a project until it has
been completed, placed at the target repository's root, referenced by package metadata,
and included in the published artifact. See the [licensing standard](../standards/licensing.md)
for the validation checklist.

### LICENSE.template replacements

Replace all of the following placeholders; none are optional:

- `{{SOFTWARE_NAME}}` — the name of the software the license covers.
- `{{LICENSOR_NAME}}` — the copyright holder granting the license (appears twice).
- `{{YEAR}}` — the copyright year.

### LICENSE.template sources and modifications

The template combines two legal texts:

- [Commons Clause License Condition v1.0](https://commonsclause.com/), reproduced
  unmodified and prepended as the condition notice, as its instructions require.
- [The MIT License](https://opensource.org/license/mit), reproduced with two deliberate
  modifications that bind the two texts together: the permission grant is made
  "subject to the Commons Clause License Condition above", and the notice-preservation
  sentence also requires the Commons Clause License Condition notice to be included in
  copies. The canonical MIT text contains neither reference.

Do not make further changes to either legal text without appropriate legal review, and
record any approved change here and in a new or superseding ADR.
