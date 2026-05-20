# Migration Step 01: node 16.13.2 migration requirements

## Scope

- Plan: adumeige/spring-boot-angular · node 16.13.1->16.14.2 · 2026-05-20T12:41
- Step: 1 of 2
- Component: node
- Version: 16.13.1 -> 16.13.2
- Category: BEHAVIORAL_CHANGE
- Kind: bump

## Objective

Update the repository so the codebase is compatible with node 16.13.2 for this migration step. Keep the change focused on the requirements listed below and avoid unrelated refactors.

## Implementation Plan

1. Inspect the repository for code, build files, configuration, tests, and documentation that reference the surfaces below.
2. Apply the required source, dependency, configuration, or test changes for this step.
3. Run the narrowest relevant verification available in the repository, then broaden only if the change touches shared behavior.
4. Commit only the files required for this step.

## Required Changes

- [16.13.2] BEHAVIORAL_CHANGE: Multi-value Relative Distinguished Names no longer accepted in certificate subjects/issuers. Node.js 16.13.2 no longer accepts multi-value Relative Distinguished Names (RDNs) in certificate subjects/issuers to prevent injection attacks (CVE-2021-44533). If your code relies on Node.js presentation of multi-value RDNs, update your certificate handling or use `--security-revert`.
  - Search hint: cve: CVE-2021-44533
  - Search hint: flag: --security-revert
  - Evidence: https://nodejs.org/en/blog/release/v16.13.2
- [16.13.2] BEHAVIORAL_CHANGE: SAN string injection fix: escape problematic characters in certificate alternative names. Node.js 16.13.2 escapes problematic characters in Subject Alternative Names (SANs) when converting to a string format to prevent injection attacks (CVE-2021-44532). If your code parses SAN strings from TLS certificates, verify that the new escaping does not break your logic; revert with `--security-revert` if necessary.
  - Search hint: cve: CVE-2021-44532
  - Search hint: flag: --security-revert
  - Evidence: https://nodejs.org/en/blog/release/v16.13.2
- [16.13.2] BEHAVIORAL_CHANGE: URI Subject Alternative Names (SANs) disabled for hostname verification. Node.js 16.13.2 disables URI Subject Alternative Name (SAN) types when checking a certificate against a hostname (CVE-2021-44531). If your code relies on URI SANs for certificate verification, grep for `checkServerIdentity` or TLS connection code; you may need to use `--security-revert` or update certificate configurations.
  - Search hint: cve: CVE-2021-44531
  - Search hint: flag: --security-revert
  - Evidence: https://nodejs.org/en/blog/release/v16.13.2
- [16.13.2] BEHAVIORAL_CHANGE: console.table() uses null prototype to prevent prototype pollution. Node.js 16.13.2 uses a null prototype object for properties assigned via `console.table()` to prevent prototype pollution (CVE-2022-21824). If your code passes user-controlled data as the `properties` parameter to `console.table()`, review that the change does not affect your output.
  - Search hint: cve: CVE-2022-21824
  - Evidence: https://nodejs.org/en/blog/release/v16.13.2

## Repository Search Hints

- covers 1 version
- 4 requirements
- cve: CVE-2021-44531
- flag: --security-revert

## Primary Evidence

- https://nodejs.org/en/blog/release/v16.13.2

## Done When

- The repository no longer contains code or configuration that violates the required changes for this step.
- Relevant tests or build checks pass, or any remaining failure is documented with the next concrete action.
- The change is committed as one focused migration step.
