<div align="center">

# Tripwire

<h3>Canary documents for RAG</h3>

[![Status](https://img.shields.io/badge/status-design%20stage-orange?style=flat-square)](ROADMAP.md)
[![Go 1.26+](https://img.shields.io/badge/go-1.26+-00ADD8?style=flat-square)](https://go.dev/dl/)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue?style=flat-square)](LICENSE)

---

[How it works](#how-it-works) · [Thesis](THESIS.md) · [Roadmap](ROADMAP.md) · [Contributing](CONTRIBUTING.md) · [Security](SECURITY.md)

</div>

---

## What is Tripwire?

Canary documents for retrieval-augmented generation (RAG). `tripwire` plants
unique, synthetic records in your vector stores, one per permission boundary,
tenant or retrieval path. If a canary ever shows up where it shouldn't (in a
model output for the wrong user, a log, a trace, outbound traffic, or another
tenant's answer), you know a boundary failed, and you know which one.

> **Status: design stage.** There is no code yet. The commands and output
> below are the proposal, and they will change. Part of the
> [OpenAstra](https://openastra.org) research agenda, area IX: AI Data
> Security & Privacy.

---

## The problem

RAG leaks are silent. When a retriever returns a document the user shouldn't
see, nothing errors: the model just answers. Teams find out from a customer,
if at all. Honeytokens (decoy credentials that alert when used) are a proven
way to detect breaches, but nobody applies the idea to retrieval systems,
which is where AI data leaks actually happen.

---

## How it works

1. **Map boundaries.** Declare what should be separated: tenants, ACL groups,
   data classes, regions.
2. **Generate canaries.** For each boundary, generate realistic synthetic
   documents containing a unique marker (a fake project name, an account
   number, a phrase) that never appears anywhere else.
3. **Plant.** Insert the canaries through your normal ingestion path, with the
   permissions of the boundary they guard.
4. **Watch.** Scan model outputs, logs, traces and egress for any marker.
   Optionally probe: run queries as users on the *other* side of each boundary
   and check whether the canary comes back.
5. **Alert with location.** A hit names the boundary, the canary, and where it
   surfaced.

---

## Example (proposed)

```console
$ tripwire probe --boundary tenants
probing 48 tenant pairs ...
LEAK   canary TW-7c19 (tenant: acme) retrieved for user in tenant: globex
       query: "what were last quarter's renewal numbers?"
       retriever: support-rag / index: kb-shared / top-k position 3
       likely cause: kb-shared ingested without tenant filter

1 leak across 48 pairs.
```

---

## Planned surfaces

- Connectors for common vector stores (pgvector, Qdrant, Weaviate, Pinecone, Elasticsearch)
- Output and log scanners as a library, an OpenTelemetry processor and a proxy
- Scheduled probing in CI or as a cron job
- Alerts to webhooks, Slack and SIEM formats

---

## Maps to

| Framework | Items |
|-----------|-------|
| OWASP LLM Top 10 (2025) | LLM02 Sensitive Information Disclosure, LLM08 Vector and Embedding Weaknesses |
| NIST SP 800-53 Rev. 5 | SC-26 Decoys, SI-4 System Monitoring, AC-4 Information Flow Enforcement |

---

## Design principles

- **Canaries must be unmistakable and harmless.** Synthetic, unique, and never real data.
- **A hit is evidence, not a guess.** No false positives from similar text.
- **Cheap to run continuously.**

---

## Roadmap

The plan, from the first working version to 1.0, is in [ROADMAP.md](ROADMAP.md). The reasoning behind the project, and what would make us stop, is in [THESIS.md](THESIS.md).

---

## Related OpenAstra projects

- [ACLDrift](https://github.com/sadayamuthu/acldrift): finds permission gaps before they leak; Tripwire proves when one did
- [anySQL](https://github.com/sadayamuthu/anysql): search traces for canary hits with SQL
- OpenEQ (in the lab): egress records to scan

---

## Contributing

Design feedback, real-world cases and fixes are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for how to help while the project is at the design stage, and [GOVERNANCE.md](GOVERNANCE.md) for how decisions are made.

---

## Security

Please report vulnerabilities privately through [GitHub security advisories](https://github.com/sadayamuthu/tripwire/security/advisories/new), not in a public issue. See [SECURITY.md](SECURITY.md) for what to include and what's in scope.

---

## License

[Apache License 2.0](LICENSE)

---

<div align="center">

**Tripwire: canary documents for RAG**

Tripwire is managed by [OpenAstra](https://openastra.org)

[GitHub](https://github.com/sadayamuthu/tripwire) · [Thesis](THESIS.md) · [Roadmap](ROADMAP.md)

</div>
