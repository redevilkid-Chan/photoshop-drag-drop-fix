---
name: Feature Request
about: Suggest a new root cause or improvement to the diagnostic
title: "[FEAT] <short description>"
labels: ["enhancement"]
assignees: []
---

## What you want

Describe the new root cause, additional diagnostic step, or improvement. Be specific:

- Is this a **new root cause** not currently in the 3-step tree?
- Is this an **additional check** that should be added to an existing step?
- Is this a **format / UX** change (e.g., different output style, additional language)?

## Why this would help

- **Frequency**: How often does this root cause / scenario occur? (rare / occasional / common)
- **Symptom**: What does the user see? (red ❌ icon / silent failure / error message / etc.)
- **Evidence**: Microsoft KB / Adobe Community / forum link confirming this is a real cause

## Suggested fix path

If you know what to check or fix, describe it:

- **Step number** (1 / 2 / 3 / Fallback) this should belong to
- **Risk level** (Low / Medium / High)
- **Exact commands or registry path**

## Alternatives considered

(Optional) Other ways to detect or fix the same root cause, and why this approach is better.

## Checklist

- [ ] I searched [existing issues](https://github.com/redevilkid-Chan/photoshop-drag-drop-fix/issues) and found no duplicate
- [ ] I linked the Microsoft KB / Adobe Community / forum source for the new root cause (if applicable)
- [ ] I am willing to test the change on my own machine before the PR (if implementing)