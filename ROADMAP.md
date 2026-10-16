# Roadmap — optional global "self-improving" data (design, not built)

The shipped tool **learns locally only**: your own logged games (combo + review score) power the
repeat-game penalty and personal insights, entirely in your browser. That is private, free, and needs
no server.

A **global** version — "collect everyone's {genre, topic, platform, audience, review-score} and tune the
shared parameters from real play" — was evaluated and **intentionally not built** for the initial free
release, because:
- **GitHub Pages is static** — there is no server to receive or store submissions.
- It introduces **privacy/legal** obligations (a privacy policy, a data controller, IP handling) and
  **abuse** risk (users can submit fake data to poison the algorithm).

If you ever want it, here is a safe design.

## Architecture
- **Serverless ingest** (e.g. Cloudflare Workers + D1/KV, or Supabase Edge Functions + Postgres with
  Row-Level Security). Generous free tiers.
- **Write path** (public): validate → store one row per submission.
- **Read path** (public, cached): serve only the **aggregated** parameters, never raw rows. The static
  tool fetches this read-only aggregate at build time or on load — keeping the client itself static.

## Anti-fake-data safeguards (the important part)
- **Server-side validation, fail-closed:** score must be in range; genre/topic/platform/audience must
  exist in a server-held whitelist; the combination must be a real, possible combo. Never trust the client.
- **Robust aggregation, not the mean:** use the **median** (or a trimmed mean) for the central value and
  **MAD-based outlier rejection** (modified z-score `0.6745·|x−median|/MAD > ~3.5` → drop). MAD has a 50%
  breakdown point: up to half the data can be garbage and the estimate still holds.
- **Minimum sample-size gating:** don't publish/trust a combo's aggregate until it has ≥ N independent
  submissions (e.g. 20–50). Below that, fall back to this tool's reconciled baseline.
- **Per-contributor weight cap + rate limiting:** cap how much any one session/identity can influence a
  combo; throttle per session token (e.g. Cloudflare Turnstile) so one actor can't spam a combo.
- **Proof-of-humanity:** optional CAPTCHA/Turnstile or lightweight proof-of-work to raise the cost of
  mass submission.
- **Dedup:** collapse identical/rapid repeats; one nonce per legitimate game-completion event.

## Privacy notes for the global version
- Combo + review-score **alone is non-personal** aggregate data — low GDPR risk.
- **IP addresses are personal data** (CJEU *Breyer*). If used for rate limiting, **don't persist raw
  IPs** (hash/truncate, or rely on edge throttling), keep retention minimal, and disclose it.
- A global version would need its own privacy policy and a consent step for the (non-essential)
  contribution — this is why it is **opt-in and separate** from the strictly-functional local storage
  the tool uses today.

Until then: the local repeat-penalty + your own logged scores give you most of the practical benefit
with none of the risk.
