Hi r/ClaudeAI,

I’ve been building a custom toolkit of Skills to make Claude's autonomous runs more reliable and its output less generic. Instead of relying on one massive system prompt, I split these into 7 distinct skills that trigger exactly when needed.

If you're building your own custom instructions or using Claude Code / agentic workflows, here is my complete setup and the core rules I use for each.

1. Verify Before Done (verify-before-done.skill)
The Problem: "No error" is not the same as "done." Claude often hallucinates success just because a tool didn't throw an exception.
The Rules:

Completeness: Walk back through every section or tab to ensure it's actually filled, not just a placeholder.
Visual Match: Look at the actual rendered output or screenshot to ensure it makes sense.
Confirmed Action: Look for a real success signal (changed URL, updated state, success toast).
Retry Once: If a check fails, retry the specific step once. If it fails again, stop and report the blocker instead of looping.
2. Ask First (ask-first.skill)
The Problem: Guessing wrong on a 20-minute agentic run costs the whole run.
The Rules:

Stop and ask 2-4 concrete, batched questions before starting any long-running task with ambiguous scope.
Offer a short list of options rather than open-ended questions.
Lead with a best guess so the user can just confirm.
Limit: Do NOT use this for quick replies or simple one-shot requests—make an assumption and go.
3. Budget Guard (budget-guard.skill)
The Problem: Small tasks can balloon into massive token sinks if Claude gets stuck.
The Rules:

Set a rough effort budget (tool calls/time) before starting.
Check progress at natural phase boundaries.
Stop and ask for direction if the task starts looping (retrying the same failed approach) or over-verifying.
If a task is genuinely complex and making real progress, raise the ceiling and keep going.
4. Plan and Verify (plan-and-verify.skill)
The Problem: Diving straight into complex, high-stakes tasks without a map leads to expensive rewrites.
The Rules:

Plan the approach before building.
Check the plan mechanically against the actual original request, not against generic self-review (which misses its own blind spots).
Verify the final finished result against the original question before calling it done.
5. Copywriting Framework (copywriting-framework.skill)
The Problem: AI defaults to generic, superlative-heavy marketing filler that talks about the product instead of the user.
The Rules:

Always determine the reader's awareness level (Unaware to Most-aware) before writing the opener.
Pick one structure (AIDA or PAS) and stick to it end-to-end.
Use specific numbers over vague claims (e.g., "34% more replies" instead of "boosts productivity").
Name the reader's strongest objection directly in the copy and handle it.
6. Creative Energy & Motion (creative-energy.skill)
The Problem: Flat, uniform pacing reads as AI-generated.
The Rules:

Use contrast and escalation. A calm section makes the urgent section stand out.
For video/motion: cut on action, vary shot length, build toward a peak.
For UI/explainers: lead with the most visual element, let visual hierarchy do the organizing, and provide one clear next step.
7. Screenshot Docs (screenshot-docs.skill)
The Problem: Auto-generated visual guides are often just a stack of full-screen captures with useless descriptions.
The Rules:

One screenshot per actual decision point.
Crop or annotate (arrows/highlights) the relevant region—no full-screen captures that bury the point.
Captions must say what to do ("Click Export, top right"), not what the image shows ("This is the export screen").
I hope these help some of you tame your workflows! Let me know if you have any questions or if you have similar skills you rely on.
