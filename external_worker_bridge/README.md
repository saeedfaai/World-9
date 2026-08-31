# World 9 External Worker Bridge

Status: TRANSPORT_MIRROR_ONLY / NON-CANONICAL / NO-RUNTIME-AUTHORITY

This public bridge exists only so an external model/provider that cannot read the private `saeedfaai/world-9-runtime` repository can obtain a source-bound onboarding/task transport snapshot.

It is **not** Project Control truth, a sixth W8 plane, a canonical writer, an authority source, or a promotion surface.

Authoritative Development-control source remains the private repository/ref named inside each bridge manifest. Titi/Project Control mirrors only the minimum non-secret material needed for the external worker to identify itself and perform the explicitly allowed bounded cycle.

Rules:
- Never place secrets, credentials, private challenges, production data, or runtime authority tokens here.
- Every mirrored item must name the upstream private ref/commit/blob hashes it represents.
- A bridge snapshot may be stale; stale or contradictory data fails closed.
- Provider connectivity does not create authority.
- Candidate/source writes are NOT authorized by this bridge unless a future explicit governed transport permit says so.
- Architecture is not weakened to fit a provider; transport is replaceable.
