# Management Evolution → AI-Native Orgs → CTO Positioning

*Working extract — June 2026*

---

## 1. Management 1.0 → 4.0 (and beyond)

**Caveat:** 1.0–3.0 is one coherent framework (Jurgen Appelo's *Management 3.0*). 4.0+ is used loosely by different communities and isn't a single agreed-on model.

- **1.0 — "do the wrong thing":** Command-and-control, hierarchy, Taylorism. People as cogs, top-down decisions. Industrial-era default.
- **2.0 — "do the right thing wrong":** Recognizes people matter, but bolts add-ons (Six Sigma, Balanced Scorecard, TQM, MBO, servant-leadership rhetoric) onto a still-hierarchical structure. 1.0 + accessories.
- **3.0 — "manage the system, not the people":** Orgs as complex adaptive systems/networks. Manager grows the system and energizes people; intrinsic motivation, empowered teams, distributed leadership. Pairs with agile.
- **4.0 — networked / digital era (fuzzier):** Tied to Industry 4.0 and VUCA. Self-organizing networks, agile-at-scale, ecosystems, data/AI-augmented decisions. Heavily overlaps 3.0; more evolution than clean break.
- **5.0 / future (speculative):** No consensus. Threads: AI as co-manager / human-AI teaming, regenerative & stakeholder-driven orgs, decentralized (DAO-like) governance, well-being at the center. Direction-of-travel, not an established model.

---

## 2. The actual shift AI introduces

- **Review over creation flips the bottleneck.** Old constraint = production capacity (how fast can we build). New constraint = **verification capacity** (how fast can we trust). Scarce resource becomes senior judgment, not hands — and judgment doesn't scale by hiring juniors, which breaks the classic pyramid.
- **Faster divergence is the real governance threat.** Three people with agents go 10x — and diverge 10x faster. Sprint-cadence sync is too coarse. Alignment moves from *periodic* to *architectural*: constrain divergence through interfaces, contracts, and guardrails **upfront**, not in review.
- **Small-team/big-scope creates a legibility crisis.** A 4-person team owning what was 20 people's surface area is great for velocity, terrible for "can anyone else understand what they did." QA/QC gates aren't just quality control — they keep the system legible to the org.
- **Watch-out:** Gates are a *leadership design decision*, not something to delegate to the agents. Agents will happily generate the tests that pass their own code.

---

## 3. Foundational literature

**First-hand empirical (highest signal):**
- Anthropic — *How Anthropic teams use Claude Code* (PDF + claude.com writeup). Ten departments, what worked and didn't. Key finding isn't speed; it's confidence in unfamiliar territory + collapse of context-switching overhead.
- Anthropic Engineering — *Building a C compiler with a team of parallel Claudes*. The task verifier must be near-perfect or the agent solves the wrong problem. QA/QC point proven at the limit.
- Anthropic Engineering — *Scaling Managed Agents: decoupling the brain from the hands*. Governance pattern for long-running agents (credentials vaulted, agent never touches them; durable sessions).

**Org-design frameworks:**
- McKinsey — *The agentic organization: contours of the next paradigm* (Sept 2025). Org charts pivot from hierarchical delegation to agentic networks / "work charts"; governance becomes real-time, embedded, with humans holding final accountability.
- Deloitte — *The great rebuild: architecting an AI-native tech organization* (Feb 2026). Tech-org specific, survey-backed.
- Reforge — *AI Native Product Teams*. Role-blurring (PMs coding, engineers doing product); keeping small-team "founder intuition" as you scale.

**Risk literature (anti-Kool-Aid):**
- *Engineering Management 2026: Structuring an AI-Native Team*. The "Talent Hollow" — kill the junior rung and you get an inverted pyramid. Fix: recast juniors as verifiers/spec-owners, not code generators.

**The edge none state loudly enough:** This is fundamentally an **interface and standards problem**. Orgs that win aren't the ones with the best prompts — they're the ones whose contracts, schemas, and guardrails constrain divergence upfront.

**On the Anthropic hypothesis:** Best *leading indicator for engineering-org design* (they dogfood frontier models, strongest incentive, earliest access). But biased sample — their pain is concentrated in software R&D, the most AI-legible domain. Other functions and regulated industries hit different walls.

---

## 4. CTO / Head of Engineering positioning

**Thesis (one-liner):**
> The engineering bottleneck has moved from production to verification. I build orgs designed around that — small teams with outsized scope, held together by hard interfaces and real-time governance instead of process ceremonies. That's how you move 10x faster without diverging 10x faster.

**Three proof-pillars:**
1. **Governance at scale is native.** Years owning group-wide API, messaging, IAM, and security standards across 20+ teams at a TSO. Constraining divergence upfront *is* the standards problem — the load-bearing capability for AI-native orgs.
2. **Operates AI-native, not theorizes.** Personally runs agents, Claude Code, verification-first workflows. Can describe the day-to-day operating model from lived experience.
3. **Domain credibility in three verticals** — energy (Elia), medtech (FibriCheck + warm network), sports-tech (personal depth).

**The wedge:**
Most CTO candidates are either deep technologists who've never run an AI-native org, or AI-hype people with no governance spine. The rare both: **enterprise-grade governance + hands-on agentic practice.**

> Tagline: *"I make small, AI-augmented teams safe to run fast."*

**Audience emphasis (same pitch, different weight):**
- Scale-up founder/CEO → velocity + not breaking things while growing.
- Board / investors → risk, governance, capital efficiency.
- Exec-search & fractional networks → crisp, repeatable one-paragraph positioning.

---

## Open thread
Sharpen the pitch for which audience first — founder/CEO, board/investors, or exec-search networks?
