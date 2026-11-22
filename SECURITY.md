# Security Policy

## Reporting a vulnerability

Please don't report security problems in a public issue, pull request or
discussion. Use
[**Report a vulnerability**](https://github.com/sadayamuthu/tripwire/security/advisories/new)
on the repository's Security tab instead. Only the maintainers can see the
report.

Include what you can of:

- the Tripwire version (`tripwire version`) or commit, your Go version and OS
- how Tripwire was used, and its configuration with secrets removed
- steps to reproduce
- what happened and what you expected

You'll get a reply when the report has been read, and again when a fix is
ready. A fix ships as a patch release; the advisory names you unless you'd
rather it didn't.

## Supported versions

Tripwire is at the design stage and has no releases yet. Once it does,
fixes land in the latest release only, until 1.0.

## What counts

Tripwire inserts synthetic documents into your indexes through your ingestion path, scans outputs and logs for markers, and can run probe queries as users on the other side of each boundary.

Tripwire is a security tool, so anything that breaks one of these promises
is a security issue:

- **Canaries are synthetic.** Canaries never contain real data. A path that copies real data into a canary is in scope.
- **The marker registry is protected.** Knowing the markers lets someone evade detection. A path that exposes the registry is in scope.
- **Probing uses only the identities you configure.** A probe that acts as anyone else is in scope.

These are by design, and not vulnerabilities:

- Canaries are visible to anyone allowed to retrieve them; that's how they work.
- A hit is evidence of a leak, not of how it happened. Investigate the boundary it names.

A wrong result that isn't covered above is a bug, not a vulnerability. Report
it in a normal issue; see [CONTRIBUTING.md](CONTRIBUTING.md).
