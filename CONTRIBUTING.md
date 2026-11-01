# Contributing to OpenPacker-Labs

OpenPacker is the reference implementation of PREX. Keep PREX contracts
vendor-neutral, preserve native package bytes, and keep Epoch or other
downstream architecture outside production packages.

Human documentation starts at
[`docs/README.md`](https://github.com/OpenPacker-Labs/OpenPacker/blob/main/docs/README.md).
Product workflows live under
[`docs/product/`](https://github.com/OpenPacker-Labs/OpenPacker/tree/main/docs/product);
API/CLI compliance rules are in
[`docs/product/compliance.md`](https://github.com/OpenPacker-Labs/OpenPacker/blob/main/docs/product/compliance.md).
Runnable samples are under
[`examples/`](https://github.com/OpenPacker-Labs/OpenPacker/tree/main/examples/README.md).
Documentation changes must pass `npm run test:docs` in the OpenPacker repository.

Agent coordination uses the org **sdlc** skill (mirrored in `.agents/skills/sdlc`
and `.claude/skills/sdlc` in this repository) plus **gh-stack**. See
[`AGENTS.md`](AGENTS.md). After editing a skill tree, run
`node scripts/check-skill-mirrors.mjs` and keep both mirrors byte-identical.

Pull request CI on OpenPacker uses affected-only Turbo scope; the merge queue
runs the full gate. Optional local review attestation:
[gh-signoff](https://github.com/basecamp/gh-signoff)
(`gh extension install basecamp/gh-signoff`). CI remains authoritative — see
[`docs/guides/ci-optimization.md`](https://github.com/OpenPacker-Labs/OpenPacker/blob/main/docs/guides/ci-optimization.md).

## Development

Use Node `^22.19.0 || >=24`, npm workspaces with the committed lockfile, stable
Rust 2024, and the checked-in tool configuration. Install with `npm ci`. The
mandatory checks and demo are offline after prerequisites are installed.

Public protocol changes start in `spec/prex/v1` and its JSON Schemas. Regenerate
consumers, repair OpenAPI/AsyncAPI, conformance vectors, TypeScript/Rust
bindings, examples, and docs in the same change. Do not hand-edit generated
files or add undeclared top-level extension fields.

Keep catalog acquisition outside the pure resolver, use the shared PURL/VERS and
canonicalization implementations, preserve native semantics with structured loss
evidence, and route one bug fix through the shared layer used by all callers.
New branches/parsers/security behavior include the smallest runnable regression
check.

## Validation

Run `npm run verify` in OpenPacker before review. It includes format, contract/generated
freshness, license, TypeScript, Rust, conformance, security, integration,
compatibility, browser, fuzz, benchmark, and production-path demo gates. Live
public providers and registries are separate opt-in jobs and do not excuse an
offline failure.

The detailed contract and release checklist is
[`docs/operations/contributing-releasing.md`](https://github.com/OpenPacker-Labs/OpenPacker/blob/main/docs/operations/contributing-releasing.md).

## AI-assisted contributions

Contributions may be built with coding agents under human direction and review.
Disclose significant AI-generated content in the pull request description.
Commits made with an agent should name the tool or model in the commit message
or in the pull request body.
