# Custom Claude Skills Toolkit

A collection of 7 custom Claude Skills to improve agentic workflows, reasoning, and output quality. 

Instead of relying on one massive system prompt, this toolkit splits instructions into 7 distinct skills that trigger exactly when needed. This makes Claude's autonomous runs more reliable, cost-effective, and its output less generic.

## The Skills

### 🛡️ `verify-before-done.skill`
**The Problem:** "No error" is not the same as "done." Claude often hallucinates success just because a tool didn't throw an exception.
* **Completeness:** Forces Claude to walk back through every section/tab to ensure it's actually filled.
* **Visual Match:** Requires checking the actual rendered output or screenshot.
* **Confirmed Action:** Looks for a real success signal (changed URL, updated state).
* **Retry Guard:** Retries a failed step exactly *once* before stopping to report the blocker.

### ❓ `ask-first.skill`
**The Problem:** Guessing wrong on a long agentic run wastes the entire run.
* Stops to ask 2-4 concrete, batched questions before starting any long-running task with ambiguous scope.
* Offers a short list of options rather than open-ended questions.
* Leads with a best guess so the user can quickly confirm.

### 💰 `budget-guard.skill`
**The Problem:** Small tasks can balloon into massive token sinks if Claude gets stuck in a loop.
* Sets a rough effort budget (tool calls/time) before starting.
* Checks progress at natural phase boundaries.
* Stops and asks for direction if the task starts repeating the same failed approach or over-verifying.

### 🗺️ `plan-and-verify.skill`
**The Problem:** Diving straight into complex, high-stakes tasks without a map leads to expensive rewrites.
* Plans the approach *before* building.
* Checks the plan mechanically against the **actual original request**, not against generic self-review (which misses its own blind spots).
* Verifies the final finished result against the original question before calling it done.

### ✍️ `copywriting-framework.skill`
**The Problem:** AI defaults to generic, superlative-heavy marketing filler that talks about the product instead of the user.
* Determines the reader's **awareness level** (Unaware to Most-aware) before writing.
* Enforces a single structure (AIDA or PAS) end-to-end.
* Uses specific numbers over vague claims and handles objections directly in the copy.

### ⚡ `creative-energy.skill`
**The Problem:** Flat, uniform pacing reads as AI-generated.
* Applies contrast and escalation (e.g., a calm section makes an urgent section stand out).
* **For video/motion:** Cuts on action, varies shot length, builds toward a peak.
* **For UI/explainers:** Leads with the most visual element and lets visual hierarchy do the organizing.

### 📸 `screenshot-docs.skill`
**The Problem:** Auto-generated visual guides are often just stacks of full-screen captures with useless descriptions.
* Enforces one screenshot per *actual* decision point.
* Requires cropping or annotating the relevant region (no full-screen captures that bury the point).
* Captions must say *what to do* ("Click Export, top right"), not what the image shows.

## Usage
Add these `.skill` files to your Claude environment or custom agent framework to give the model concrete guardrails against common failure modes. 
