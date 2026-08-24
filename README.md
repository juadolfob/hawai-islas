# 🌺 Hawaii 2026 — a trip planned with AI

> Full planning record for a family trip to **Oʻahu** (Aug 17–22, 2026, five adults),
> put together with an AI assistant — from "which island?" all the way to a locked-in
> day-by-day itinerary.
>
> All personal data has been replaced with placeholders. See [Privacy](#-privacy).

**Live site:** https://juadolfob.github.io/oahu-2026-ai-planned-trip/

---

## What this is

Not a travel blog. This is the **work trail** of planning a family vacation with AI as a
copilot — the data, the comparisons and the decisions, written down as they happened.

It started with one question (*which island do we go to?*) and ended with a closed
itinerary: bookings made, budget verified, and a voting app so all five could weigh in.

## How it was built

**1. Research → structured data.**
Instead of scattered notes, everything went into YAML: islands, hotels, tours, prices,
booking windows, overlaps between activities. One file as the source of truth
([`data/itinerary_2026.yaml`](data/itinerary_2026.yaml), ~1,700 lines).

**2. Data → site.**
The HTML pages were generated from that YAML: island comparison, attraction catalog,
lodging comparison and a visual itinerary. Everything is self-contained — the pages open
straight in a browser, no server needed.

**3. Deciding as a family.**
The real problem was never finding things to do, it was **choosing among too many**.
So we built a star-voting system across 115 activities: each person picked "who am I"
and rated. Votes lived in a Realtime Database so all five stayed in sync live.

**4. Overlap pruning.**
The most useful and least obvious part: spotting how much was **already included**
elsewhere. The Circle Island Tour already covered Diamond Head, Halona Blowhole,
Makapuʻu, Dole and Sunset Beach; the Toa Lūʻau bundled entry to Waimea Valley.
Flagging those overlaps avoided paying twice and freed up entire days.

**5. Trip log.**
During the trip we recorded what actually happened
([`docs/trip-log.md`](docs/trip-log.md)) against what was planned.

## What's in here

| File | What it is |
| --- | --- |
| [`index.html`](index.html) | Island comparison — the landing page |
| [`attractions.html`](attractions.html) | Attraction and tour catalog, with star voting |
| [`lodging-comparison.html`](lodging-comparison.html) | Hotel comparison |
| [`itinerary.html`](itinerary.html) | Visual itinerary |
| `data/` | YAML sources |
| `docs/` | Working notes, plan status and trip log |
| `img/` · `audio/` | Site assets |

> Don't move `img/` or `audio/` — the HTML references those paths directly.

## The voting, frozen

Votes lived in a realtime database so the family could vote from their phones and see
changes instantly. Once the trip ended the database was shut down and **the final results
were embedded directly into the HTML**.

The interface still works: you can pick who you are and vote, but it now saves only to
your browser (`localStorage`). No backend, no keys, nothing to maintain.

## 🔒 Privacy

This repo was private during planning because it held real data. Before going public,
**all personal information was replaced**:

- Names → generic roles (`Dad`, `Mom`, `Kid 1`, `Kid 2`, `Kid 3`)
- Booking codes, airline PNRs and confirmation numbers → `XXXXXX`
- Emails, phone numbers, birth dates and loyalty numbers → placeholders
- Confirmation PDFs and the payment report were deleted
- The database configuration was removed

Git history was rebuilt from scratch, because deleting files isn't enough — the data
stays recoverable in earlier commits.

Prices, schedules, routes and opinions about places are real — that's the part that
might actually be useful to someone else.

## If you're planning your own trip

Usable as-is: the island comparison, the attraction catalog with prices and ratings,
the Waikīkī hotel comparison, and above all the **overlap analysis** — which tours
step on each other and what's already bundled into what.
