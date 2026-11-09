# Contributing

Thanks for helping make the console easier to use and its limitations clearer.
This repository contains a prebuilt static site, not the original application
source or a reproducible build environment.

## Good Contributions

- Clearer setup, hosting, troubleshooting, and accessibility documentation.
- Sanitized browser or firmware compatibility reports.
- Corrections to protocol research that identify supporting evidence and
  distinguish observations from inferences.
- Focused bug reports and feature requests with a clear user need.

Discuss application changes before submitting a replacement build. Avoid
hand-editing minified bundles: without the original source and build process,
such changes are difficult to review and reproduce. A proposed generated release
should identify its source revision and build instructions when available, its
provenance, changed behavior, and validation evidence. State missing evidence
explicitly rather than implying reproducibility.

## Reporting Bugs and Compatibility

Read the [troubleshooting table](README.md#troubleshooting) and search existing
issues first. For an ordinary public report, include:

- Browser name and version, operating system and version.
- Hosting type (for example, GitHub Pages), HTTPS status, and whether this is a
  fresh session or an update. Omit private URLs.
- Deployed commit or release identifier, if known.
- Lock model and firmware version, if known; omit serial numbers and device IDs.
- Minimal reproduction steps, expected behavior, and actual behavior.
- Sanitized visible error text and whether the physical lock performed the
  requested action despite an error.
- Whether the result was observed on physical hardware, in a simulator, or only
  inferred from research. Say "unknown" for details you cannot establish.

Never include PINs, temporary codes, credential lists, unlock history, Bluetooth
addresses, saved browser storage, or raw Bluetooth packets. Crop and redact
screenshots before uploading them. Do not upload a vendor APK or decompiled
vendor code; describe evidence and cite the existing research where possible.

For vulnerabilities, suspected credential exposure, or unauthorized access
paths, follow [SECURITY.md](SECURITY.md) instead of opening a public issue.

## Making a Pull Request

1. Create a focused branch from the current repository state.
2. Read the relevant documentation and preserve its safety warnings and
   distinction between verified behavior and assumptions.
3. Keep changes scoped to one purpose. Do not reformat generated assets or
   include editor settings, browser profiles, diagnostic dumps, or secrets.
4. Explain what changed, why, and how it was checked. Identify untested hardware
   or browser behavior explicitly.
5. Link a relevant issue when one exists. Do not claim a bug is fixed solely
   because the page renders.

## Validating Documentation Changes

No dependency installation or application build is needed for documentation-only
changes. This distribution does not include an automated test runner.

- Check relative links, filenames, and README section anchors.
- Preview Markdown tables and code fences.
- Check that instructions match the files actually present.
- Keep browser support and hardware-validation claims within the available
  evidence; do not generalize a single successful unlock to all operations.
- Review the changed file list to ensure no site files changed accidentally.

Before submitting, run:

```powershell
git diff --check
git status --short
```

`git diff --check` checks tracked unstaged changes; use
`git diff --cached --check` for staged changes. Newly created untracked files
still need review and must be intentionally added before they can be committed.

For deployment changes, also use the
[hosting verification checklist](docs/HOSTING.md#verification-checklist).
Documentation-only contributions do not require a physical lock.

## Safe Hardware Testing

Test only with explicit authorization, a physically accessible door, and an
independent means of entry. Start with read-only operations. Do not use
credential changes or factory reset as connectivity tests.

A timeout is not proof of failure: inspect the physical state before retrying.
Disconnecting or rolling back the website does not undo a command accepted by
the lock. Never test on someone else's lock to establish compatibility.
