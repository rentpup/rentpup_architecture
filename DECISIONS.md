# Decisions

The choices in RentPup that were not obvious, and what they cost.

A list of technologies says what a system is made of. This says what it had to decide. Where I got something wrong first, that is written down too.

---

## Report Unknown rather than infer

**Decision.** Where the public records do not establish an answer, the system reports the status as **Unknown**. It does not guess, and it does not treat an absent record as evidence of compliance or of violation.

**Why this is harder than it sounds.** Unknown is the worst looking cell in a table. It reads like the product failed. Every instinct says fill it, and there is usually a defensible-sounding rule available: no record found means no violation, or the last known status carries forward.

**Why I did it anyway.** The product's only value is that an owner can act on what it says. A compliance tool that is confidently wrong is worse than no tool, because it replaces uncertainty the owner knew they had with false comfort. The first time it says "compliant" about a property that is not, it is finished, and so is the customer's trust in everything else on the page.

**What it cost.** A visibly less complete product, and an explanation on the page about why a field is empty. Worth it.

---

## Hold state over time rather than look up on demand

**Decision.** The system maintains structured property records and updates them on a schedule, rather than querying the public sources fresh on each page view.

**Why.** The product exists to answer "what changed," and you cannot answer that without knowing what you previously held. A live lookup can only ever show the present, which means the owner has to notice the difference themselves, which is the job they are paying to avoid.

**Second reason, less obvious.** The sources are not fast, not consistently available, and not designed to be queried per visit. Building on demand would have made the product's reliability a function of theirs.

**What it cost.** Storage, a sync schedule to maintain, and the whole class of problems that come with holding a copy of something that changes.

---

## Normalize address to property identity before interpreting anything

**Decision.** Records from different sources are resolved to a single property identity first. Nothing is interpreted until that has happened.

**Why.** Public systems do not agree about how an address is written. The same parcel appears differently across sources, and an owner with several properties compounds it. Interpreting before resolving produces a confident answer about the wrong building, which is the worst kind of wrong because it looks right.

**What it cost.** This is the least glamorous part of the system and it took the most iteration. It is also the part that everything else depends on.

---

## Put the specific problem in the first message

**Decision.** Outreach names the property and the obligation rather than describing the product.

**Why.** An owner ignores "are you compliant with Cleveland's rental requirements" because it is addressed to everybody. They do not ignore a message about their building and their deadline.

**What made it possible.** Only that the data was already structured for the product. Doing this by hand for any real volume would not be worth the time, which is why almost nobody does it.

See [the lead engine](./LEAD-ENGINE.md).

---

## Buy the boring parts

**Decision.** Supabase, Stripe, Resend, Vercel, Sentry. Nothing self-hosted, nothing clever.

**Why.** One person. Every service I run is a service I am on call for, and none of billing, auth, transactional email or hosting is where this product is differentiated. The differentiation is in the records and what is done with them.

**What it cost.** Less control, a monthly bill, and dependence on other people's uptime. All three are cheaper than my attention.

---

## Build it with AI assistance, and be specific about what that means

**Decision.** Written with Claude Code, by one person, from concept through launch.

**What that actually covers.** The code was largely AI-assisted. The product design, the workflow architecture, the data model, the service choices, the integration work and a great deal of testing were the work, and they were mine.

**The honest division.** I architect and integrate. I am not a career software engineer, and I do not pretend the code came out of my head line by line. What I do is decide what the system must do, what it must refuse to do, how the public records actually behave, and then verify that what got built holds up against real data. That last part is most of the time.

**What it cost.** A real and ongoing need to check things. AI writes confident code that is subtly wrong more often than it writes code that obviously fails, and a compliance product is exactly where subtly wrong matters. Catching that before a customer does is a skill, and it is the one I have spent the most time developing.

---

## Open questions

Things I have not solved, listed because a decisions document that only contains wins is marketing.

**Compound parcels.** Properties that span multiple parcels, or parcels that split, are not handled cleanly yet.

**No competitive benchmark.** As far as I can tell nobody else is doing records-driven outreach in this market. That is an advantage and it also means I have nothing to measure against.

**Scale is unproven.** This runs for one county. Whether the normalization approach survives a second county with different record conventions is an open question, and I would expect it to need work rather than to just extend.

---

Back to the [architecture overview](./README.md).
