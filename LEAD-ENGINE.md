# The lead engine

How RentPup finds the people who need it.

The product watches public records so an owner learns about a compliance problem before it becomes a violation. Those same records say who else has a problem. The lead engine is the second use of the first system.

It runs unattended.

---

## The idea

Most outbound in this market is a list of property owners and a generic pitch. That is a guess dressed up as targeting: it knows who owns property, not who has a problem.

The records already contain the answer. Rental registration, lead-safe certification, Local Agent in Charge filings and court activity each say something about whether an owner is currently exposed. An owner with an open issue and a deadline approaching is in a different situation from an owner who is current on everything, and the difference is visible in the data before anyone is contacted.

So the engine does not ask "who owns rental property in Cleveland." It asks "whose records indicate a problem worth paying to solve."

---

## What it reads

The same normalized property state the product runs on. Nothing separate is scraped for sales purposes, which matters for two reasons: the sales data is exactly as current as the product data, and there is only one place where an address gets resolved to a property identity.

Most properties here are held under LLCs rather than personal names, so the entity holding the property and the person who would buy the software are not automatically the same record. Resolving that relationship is part of the work.

---

## How it prioritizes

Ranking is by how strongly the records indicate a present problem, not by portfolio size or any proxy for ability to pay. A single-property owner facing a lead-safe deadline is a better contact than a large portfolio that is current on everything, because the first one has a reason to act this month.

The ranking exists because attention is the scarce resource. Contacting everyone is the same as contacting no one, and a list sorted by nothing is a list sorted by accident.

---

## What goes into the outreach

The specific issue, on the specific property.

Not "are you compliant with Cleveland's rental requirements," which every owner ignores because it is addressed to no one in particular. The message names the property and the obligation attached to it, because that is the fact that makes someone stop and read.

This is the part that would be hardest to do by hand and is nearly free once the data is already structured. It is also the reason the engine has to sit on top of the product rather than beside it.

---

## Measurement

There is a direct mail measurement and attribution system, so physical outreach can be tied back to the accounts it produced rather than assumed to have worked.

Direct mail is the format where attribution is usually abandoned. Skipping it means never knowing which of two approaches was better, which means running the worse one indefinitely.

---

## What I would tell you it does not do

It does not decide who is worth contacting based on anything the records do not support. The same rule that makes the product report **Unknown** rather than infer a compliance status applies here: an owner whose records are thin is not scored as though the absence of a problem were evidence of one.

It does not personalize beyond the fact. There is no generated flattery and no invented context. The personalization is that the message is true about that property, which turns out to be enough.

It has not been tested against a serious competitor doing the same thing. As far as I can tell nobody in this market is doing it, which is an opportunity and also means I have no benchmark.

---

## Why this is the interesting part

The compliance product is the thing customers pay for. The lead engine is the thing that makes a one-person company viable, because it removes the step that usually requires a sales team.

It is also the part that transfers. The mechanics, taking a data source nobody has structured, resolving identity across records, scoring on a signal that predicts a real need, and putting the specific reason into the first message, are not specific to property compliance. That is a description of go-to-market engineering, and this is where I learned it.

See the [architecture overview](./README.md) for how it fits the rest of the system.
