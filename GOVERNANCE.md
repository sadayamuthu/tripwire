# Tripwire Governance

This document says who makes decisions about Tripwire, how they are made,
and how contributors become maintainers. It follows the shape of the
[Minimum Viable Governance](https://github.com/github/MVG) template, scaled to
the project's current size. It is shared, with only names and project-specific
lists changed, across the [OpenAstra](https://openastra.org) projects.

## Current state

Tripwire is a design-stage project with one maintainer (see
[MAINTAINERS.md](MAINTAINERS.md)). That is a risk, and growing past it is
the first goal of this document: the roles and processes below are written
so that new maintainers can join without changing the rules.

## Roles

**Users** use Tripwire and report what works and what doesn't. Issues,
discussions and real-world feedback are contributions. While the project is
at the design stage, feedback on the design is the most valuable kind.

**Contributors** have had at least one pull request merged, or have made
other sustained contributions (triage, documentation, design review).

**Maintainers** have write access to the repository. They review and merge
pull requests, triage issues, cut releases, and take part in decisions. The
current maintainers are listed in [MAINTAINERS.md](MAINTAINERS.md).

**Lead maintainer** is a maintainer who also holds the project's release,
domain and other accounts, and breaks ties (see below). While there is one
maintainer, that person is the lead maintainer.

## Becoming a maintainer

A contributor can become a maintainer when they have:

- had several non-trivial pull requests merged over at least two months,
- reviewed others' pull requests or triaged issues, and
- shown that they follow [CONTRIBUTING.md](CONTRIBUTING.md) and the
  [Code of Conduct](CODE_OF_CONDUCT.md).

Any maintainer may nominate a contributor, including themselves, by opening a
pull request that adds them to MAINTAINERS.md. The nomination is accepted by
lazy consensus (below) after seven days. While there is one maintainer, that
maintainer decides, and gives the reason in the pull request.

The project aims to have **maintainers from at least two organizations**,
and treats contributors from organizations not yet represented as a priority
for review and mentoring.

## Stepping down

Maintainers may step down at any time by opening a pull request that moves
them to the Emeritus section of MAINTAINERS.md. A maintainer who has not
reviewed, merged or commented for six months may be moved to Emeritus by the
other maintainers, after asking them first. Emeritus maintainers can return
through the normal nomination process.

## Decision making

Most decisions are made in pull requests and issues by **lazy consensus**:
a proposal is accepted if no maintainer objects within a reasonable time
(at least 72 hours for anything beyond a small fix).

The following need **explicit approval by a majority of maintainers**:

- changes to the marker format or registry,
- anything that could put real data into a canary,
- a 1.0 or other major release,
- adding or removing a maintainer when someone objects,
- changes to this document.

If maintainers cannot reach consensus, the lead maintainer decides and
records the reason in the issue or pull request.

## Releases

Releases are cut by maintainers by pushing a `vX.Y.Z` tag on `main`. CI
builds the binaries, attaches them to a GitHub release, and updates the
formula in [sadayamuthu/homebrew-tap](https://github.com/sadayamuthu/homebrew-tap).
There are no releases yet.

## Code of conduct

Everyone taking part in the project follows the
[Code of Conduct](CODE_OF_CONDUCT.md). Maintainers enforce it.

## Security

Vulnerabilities are reported privately and handled as described in
[SECURITY.md](SECURITY.md).

## Changes to this document

This document changes by pull request, with explicit majority approval of
the maintainers.
