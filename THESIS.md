# Tripwire: thesis

**In one line:** honeytokens work for credentials; the same idea, applied to
retrieval boundaries, turns silent RAG leaks into alerts that name the
boundary that failed.

## The problem

RAG leaks are silent. When a retriever returns a document the user shouldn't
see, nothing errors; the model just answers. Teams find out from a customer,
if at all.

## The bet

1. **A unique marker is proof.** A synthetic canary planted behind one
   boundary that appears on the other side is evidence of a leak, not a
   guess, so alerts carry no false positives from similar text.
2. **One canary per boundary localises the failure.** Planting per tenant,
   ACL group and data class means a hit names exactly which boundary broke.
3. **Probing beats waiting.** Querying as users on the other side of each
   boundary finds leaks before real users trigger them.
4. **Cheap enough to run continuously**, which is what makes it detection
   rather than an audit.

## Why now

Multi-tenant and permission-scoped RAG is now standard in SaaS and
enterprise products, and those boundaries are enforced by filters that are
easy to get wrong and rarely tested end to end.

## What success looks like

- In seeded test deployments, probing finds every introduced boundary break.
- No false-positive alerts in production use.
- Teams run scheduled probes in CI or cron and route hits to their SIEM.

## What would prove us wrong

- Canaries can't be made realistic enough to be retrieved by real queries
  without risking confusion with real data.
- Teams won't allow synthetic documents in production indexes.
- Probing needs per-user credentials that are impractical to obtain safely.

## Not a bet on

Finding permission gaps before they leak (ACLDrift) or poisoned content
(HubScan).

## Where it fits

Area IX, AI Data Security & Privacy. Proves the leaks
[ACLDrift](https://github.com/sadayamuthu/acldrift) predicts; hits are
searchable with [anySQL](https://github.com/sadayamuthu/anysql).
