# Reviewer Agents

Three reviewer personas plus a shared target profile, for getting
honest, unbiased reviews of the resume from different evaluative
perspectives.

## Files

| File | Lens |
|---|---|
| `target_profile.md` | What the candidate is targeting. Shared anchor. |
| `scaleup_ceo.md` | "Would I take the call?" — a scale-up CEO hiring for Head of Eng / CTO. |
| `beangels_investor.md` | "Would I back this person?" — a Belgian angel investor. |
| `takingturns_recruiter.md` | "Is this placeable?" — a Belgian executive search recruiter. |

## How to use (manual, today)

For each reviewer:

1. Open Claude or ChatGPT in a fresh conversation.
2. Paste `target_profile.md` as the first message.
3. Paste the reviewer file (e.g., `scaleup_ceo.md`) as the second
   message.
4. Paste the rendered resume content as the third message. Easiest
   source: open http://127.0.0.1:4000/detail/ in a browser, select all,
   copy, paste as plain text. Or copy the rendered HTML.
5. Send a final instruction: "Run the review now, using the output
   format from the reviewer file. Do not flatter."

Run each reviewer in a separate conversation so they do not contaminate
each other.

## How to use (automated, future)

Next step is a small Node or Python script using the Anthropic API that
runs all 3 reviewers in parallel against the resume content, then
collates the verdicts into a single report. Not built yet. This is the
"small agentic build" artefact track from the AI-era positioning work.

## Anti-flattery

Each persona has explicit anti-flattery rules and a scored output
structure. LLMs default to sycophancy. These prompts are designed to
push back against that and produce reviews that name specific weak
points, quote the resume directly, and refuse to call something a 5
when it is not.

## Iteration

If a reviewer's output feels too soft or too harsh, edit the persona
file directly. The personas are intentionally opinionated. Sharpen the
biases, sharpen the anti-flattery rules, sharpen the output format. Run
the review again.
