---
description: Run all 3 reviewer personas in parallel against the resume, collate verdicts
---

You are about to orchestrate **3 parallel resume reviews** using the
reviewer personas defined in `agents/`. The personas evaluate the
candidate from three perspectives: a scale-up CEO, a BeAngels angel
investor, and a Taking Turns leadership recruiter.

This is the candidate's own "small agentic build" — built as a tool to
get unbiased reviews of their resume positioning. Treat the run with
the rigor that intent deserves.

## Steps

### 1. Read all inputs first

Read in parallel:

- `tmp/private/target_profile.md` — what the candidate is targeting
- `assets/context/management-evolution-and-ai-native-org.md` — the
  candidate's strategic edge (the "review-over-creation" thesis, the
  AI-native operating model wedge). Reviewers must factor this in.
- `agents/scaleup_ceo.md`
- `agents/beangels_investor.md`
- `agents/takingturns_recruiter.md`

### 2. Fetch the rendered resume content

Curl both pages:

- `http://127.0.0.1:4000/` (one-pager — primary)
- `http://127.0.0.1:4000/detail/` (chronological — secondary)

If either returns non-200, tell the user Jekyll is not running locally
and that they should start it with `bundle exec jekyll serve`. Abort
the review.

### 3. Spawn 3 parallel subagents

Use the Agent tool (`subagent_type: general-purpose`) to dispatch 3
reviews **in a single message with 3 parallel tool calls** — they must
run independently, no cross-contamination.

Each subagent's prompt must contain:

- The full target profile content
- The full management-evolution context document
- Their respective persona file content (full)
- Both fetched resume HTML pages (one-pager + detail)
- Explicit instruction: "Produce the review in the exact output format
  specified in the persona file. Do not flatter. Quote resume evidence
  for every claim."

Each subagent returns the structured review per its persona's output
format.

### 4. Audit the reviews for sycophancy before summarising

Before producing the meta-summary, audit each returned review against
these signals of flattery:

- All scores are 4 or 5 with thin evidence
- The "what does not work" section is short, vague, or missing
- The "would not recommend a call" item is absent or hedged
- Quotes from the resume are missing or paraphrased

If a review trips any of these signals, **flag it in the meta-summary
as `[POTENTIALLY FLATTERING — interpret with skepticism]`** and quote
the soft passages.

### 5. Produce the final output

In this exact structure:

````markdown
# Resume Review · 3 Personas

## 1. Scale-up CEO Review
[the CEO subagent's full review, verbatim]

## 2. BeAngels Investor Review
[the investor subagent's full review, verbatim]

## 3. Taking Turns Recruiter Review
[the recruiter subagent's full review, verbatim]

---

## Meta-summary

### Fit scores summary
| Reviewer | Score | Recommendation |
|---|---|---|
| CEO | X/5 | Pass / Call / Lead candidate |
| Investor | X/5 | Pass / Coffee / Push to portfolio / Strong yes |
| Recruiter | X/5 | Hold / Niche match / Active pitch / Top of pile |

### Common themes
3 to 5 bullets. Things 2 or all 3 reviewers agreed on. Each with a
quote from at least 2 of the reviews.

### Highest-confidence concerns
Ranked list of concerns raised by 2 or 3 reviewers. For each:
- The concern stated once, clearly.
- Quoted evidence from each reviewer that named it.

### Top 3 action items, ranked by impact
1. **[Action item]** — which reviewer(s) flagged it. Specific suggested
   edit (before / after if applicable).
2. ...
3. ...

### Sycophancy audit
Note any reviews flagged as potentially flattering and why.
````

## Notes for the orchestrator

- Run the 3 subagents in parallel, not sequentially. Anti-flattery
  requires they cannot see each other's output.
- The candidate has invested real strategic thinking in their
  positioning (see the management-evolution context document). The
  reviews should engage that thinking, not dismiss it. But they should
  not adopt the candidate's framing wholesale either.
- The candidate's own anti-flattery clauses are baked into the persona
  files. Reinforce them in the subagent prompts.
