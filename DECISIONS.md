# Decisions

## Decision Point 1 — The Nudge

**Choice:** Encourage, don't shame or block. When the weekly target is crossed, show a neutral, informative message that names the overshoot and points to the user's largest category (e.g. *"You're 4.2 kg over target. Your biggest category this week is travel."*). The user can always keep logging.

**Why:** A carbon tracker is only useful if it keeps recording reality, including weeks where the user exceeds their target. Blocking entries after an overshoot would make the data incomplete and defeat the purpose of tracking. A calm, factual nudge that surfaces the biggest contributor is more actionable than moralizing, and it nudges behavior without creating a hostile experience that makes people stop using the app.

---

## Decision Point 2 — Absurd Input

**Choice:** Reject obviously implausible values at the form level, with a clear inline warning, and refuse to log them. Each activity type has a sensible per-entry maximum (e.g. a single car trip cannot be 500,000 km). The user is asked to check their input rather than having it silently capped.

**Why:** A tracking application is only trustworthy if its records are accurate. Silently clamping a value like 500,000 km down to some "reasonable" number would produce a footprint figure the user never actually entered, which is worse than an error. Rejecting the input with a warning keeps the data clean, makes the failure mode obvious, and avoids the absurd 100,000 kg CO₂ result that would otherwise dominate the dashboard.

---

## Decision Point 3 — The Week

**Choice:** Fixed Monday → Sunday weeks. The dashboard always shows the current Monday–Sunday window, with a continuous progress bar from Monday to today. History is grouped into completed Monday–Sunday weeks so they can be compared directly.

**Why:** A fixed, universally understood week boundary makes the dashboard predictable — users don't have to wonder what "this week" means on a Wednesday. It also makes week-over-week comparisons meaningful in the history view, since every bucket covers the same seven days. Rolling 7-day windows would be more flexible but would make both the progress bar and the history table harder to reason about at a glance.

---

## Standard API

**Not implemented.** The brief provides fixed, deterministic emission factors for every activity type, so there is no external API to conform to. CO₂ is calculated locally as `quantity × factor` and stored with each logged activity. This means grading is done by a **browser agent driving the UI** rather than by script — every feature (logging, calculating, dashboard, target, history/filter) is reachable through the interface without authentication.