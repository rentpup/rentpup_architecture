# RentPup

Compliance monitoring for rental property owners in Cleveland, Ohio.

Most rental property in Cleveland is held under LLCs, and the obligations attached to it are scattered across separate public systems: rental registration, lead-safe certification, Local Agent in Charge filings, and court activity. Owners generally find out they have a problem after a deadline has passed. RentPup watches those records continuously and tells an owner what is coming before it becomes a violation.

It is a live product with paying customers, built and operated by one person.

This repository is documentation. The application source is private, because the product is commercial.

---

## How it works

Two systems, built separately, that happen to share the same data.

### 1. The compliance engine (the product)

**Collection.** Pulls from multiple City of Cleveland and Cuyahoga County public record sources on a recurring schedule and associates each record with the right property. No owner action is required after the initial setup.

**Normalization.** Public records do not agree with each other about how an address is written, so records are normalized and matched to a single property identity before anything is interpreted.

**State over time.** Rather than performing a fresh lookup on every page view, the system maintains structured property records and updates them on a schedule. That means it can answer "what changed since last time," which is the question the product actually exists to answer.

**Interpretation, with a deliberate refusal.** Where the underlying records do not establish an answer, the system reports the status as **Unknown**. It does not infer a status the records do not support. This was a design decision rather than an omission: a compliance tool that guesses confidently is worse than one that admits what it cannot see.

**Delivery.** A scheduled job recomputes obligation statuses, identifies differences between what was previously held and what is now held, and sends deadline notifications from those differences.

### 2. The lead engine (how the product finds customers)

The same public records that tell a customer they have a problem also identify who else has one.

The lead engine reads property and compliance data, finds owners whose records indicate they are likely to need the product, prioritizes who to contact first, and attaches the specific issue to each outreach. Outreach references the actual property and the actual obligation rather than a generic pitch.

It runs unattended.

There is also a direct mail measurement and attribution system, so physical outreach can be tied back to the accounts it produced.

---

## Stack

| Layer | Choice |
|---|---|
| Application and hosting | Vercel |
| Database and auth | Supabase |
| Billing | Stripe |
| Transactional email | Resend |
| Error monitoring | Sentry |
| Analytics | Google Analytics |
| Source control | GitHub |

---

## How it was built

Written with [Claude Code](https://claude.com/claude-code), by one person, from concept through launch.

That is worth being specific about rather than vague. The work was product design, workflow architecture, data modeling, service selection, integration, and a great deal of testing and iteration. The code was largely AI-assisted. Deciding what the system should do, what it must refuse to do, how the public records actually behave, and why an **Unknown** status is better than a confident wrong one was not.

The honest division of labor: I architect and integrate. I am not a career software engineer, and the parts of this that look like software engineering were built with AI assistance and then tested against real records until they held up.

---

## Why this repository exists

Most of what I have built is either commercial or lives inside someone else's company. This is a public description of a system that is actually running, written so the design decisions are visible without exposing the product.

If you want to see the product itself, it is at [rentpup.com](https://rentpup.com).
