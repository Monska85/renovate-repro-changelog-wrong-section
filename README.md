# 46628

> **Temporary repository.** Created on 2026-10-01 only as a minimal reproduction for
> renovatebot/renovate discussion https://github.com/renovatebot/renovate/discussions/46628. It has no other purpose.
> Delete or archive it once that discussion is closed.

Minimal reproduction for Renovate discussion https://github.com/renovatebot/renovate/discussions/46628.

`deps.txt` pins `Monska85/renovate-repro-changelog-wrong-section-dep` at `0.9.0`
through a regex custom manager with the `github-tags` datasource. That
dependency repository has tags `0.9.0`, `0.9.4` and `1.0.0` and a
`CHANGELOG.md` in Keep a Changelog style, where every section has a dated
heading and an inline "Compare with previous version" link:

```markdown
## [1.0.0] - 2026-07-30

[Compare with previous version](https://github.com/Monska85/renovate-repro-changelog-wrong-section-dep/compare/0.9.4...1.0.0)

- BREAKING: this entry belongs to 1.0.0 only.

## [0.9.4] - 2026-07-28

[Compare with previous version](https://github.com/Monska85/renovate-repro-changelog-wrong-section-dep/compare/0.9.0...0.9.4)

- FIX: this entry belongs to 0.9.4 only.
```

## Current behavior

The PR that updates the dependency to `0.9.4` renders, under the `v0.9.4`
heading of the Release Notes section, the body of the `1.0.0` changelog
section ("BREAKING: this entry belongs to 1.0.0 only."), with the anchor
`#100---2026-07-30`.

The `1.0.0` section is matched because its "Compare with previous version"
line contains both the package name and the string `0.9.4`, and that section
comes before the real `## [0.9.4]` heading in the file.

## Expected behavior

The `v0.9.4` release notes show "FIX: this entry belongs to 0.9.4 only.", the
body of the section whose heading contains `0.9.4`.

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/46628
