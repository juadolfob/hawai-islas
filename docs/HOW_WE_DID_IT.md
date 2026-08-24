# 🤖 How we planned the trip with AI

Quick summary of the method. Six days in Oʻahu, five people, planned and run by talking with Claude.

---

## 1. One single source of truth

- Everything lives in **`data/itinerary_2026.yaml`**: flights, lodging, day-by-day segments, attraction catalog, bookings, risks, pending items.
- The site is generated from that file. Nothing gets edited in two places.
- Edited with `ruamel.yaml` so comments never got lost.

## 2. Delegated research

- Asked the AI to catalog **all 43 attractions covered by the Go City pass** — rating, review count, price without the pass, and whether it needed a separate reservation.
- Same for hotels, islands and Viator tours.
- Result: comparing stops being "open 30 tabs" and becomes "sort a table."

## 3. Deciding with numbers, not opinions

- The key number: **the pass cost ~$1,040 ÷ 4 slots = ~$260 per slot.**
- The rule that came out of it: **if an attraction costs less than $50, it's not worth a slot** — buy it separately instead.
- That single rule immediately ruled out $16 museums, $23 yoga classes, and cheap rentals that looked tempting.

## 4. Live family voting

- **`attractions.html`** + a **Realtime Database** (during planning).
- Everyone opens it on their phone, picks who they are, and rates with stars.
- Votes synced instantly — everyone saw everyone's preferences.
- No login, no accounts, no app. Just a link.
- **The database is off now:** the final results are embedded in the HTML and voting saves only to the browser.
- Sortable by price, rating or **demand** (how fast a slot fills up).

## 5. Overlap analysis

- Pulled the **actual** itinerary of each booked tour and cross-checked it against the catalog.
- Example: the Circle Island tour already included Halona Blowhole, Sunset Beach, Dole Plantation and the shrimp lunch — four items that were still listed separately.
- Redundant items were grayed out **with the reason written right on the card**, not deleted.
- Effect: you stop re-litigating the same choice every time you open the list.

## 6. Status visible at all times

CSS badge system on every card:

| Status | Meaning |
| --- | --- |
| 🟢 Green | Included in the pass / booked |
| 🔵 Blue | Free access, no pass needed |
| 🟡 Yellow | Included but cheap — not worth a slot |
| ⚪ Gray | Dropped, with the reason |
| 🔴 Red | Heavy overlap with something already booked |

## 7. Live assistance during the trip

The part that gave the most value wasn't the upfront planning:

- **Timed route comparisons** — H-2 vs H-3 vs the coastal route, and whether a route would cost the waterfall stop.
- **"Do we have time?" math** — 45 minutes before the lūʻau check-in, with a 20-30 min trail each way: it didn't fit.
- **Digging info out of emails** — the Kualoa waiver link buried in an operator message, found half an hour before it mattered.
- **Catching booking errors** — the fifth pass number on file turned out to be the order number, not a card number. Would have cost the full tour price.
- **Verifying instead of assuming** — opening hours, booking windows, whether a place takes walk-ins. There was almost always a detail that changed the decision.

## 8. Trip log kept separate from the plan

- **`docs/CURRENT_STATUS.md`** = the plan.
- **`docs/trip-log.md`** = what actually happened.
- Keeping them separate stops the plan from getting silently rewritten by hindsight, and makes it easy to see where the estimates were off.

---

## Mistakes we made

- **Booked the lūʻau twice** (Viator + direct). Canceled in time, and the direct booking came out $172 cheaper.
- **Underestimated check-in windows.** 45 minutes ahead, mandatory, no refund if late. True for almost everything.
- **Overplanned day 2.** It ended up being a split day where everyone did their own thing — and it was everyone's favorite.
- **The repo was public by mistake** with personal data inside. That's where the sanitization pass came from.

## What we'd do again

- The YAML as the single source of truth.
- Live voting — it turns the discussion from negotiation into consensus.
- Graying things out with the reason visible, instead of deleting.
- Asking the AI **"do we have time?"** before every decision on a clock.
