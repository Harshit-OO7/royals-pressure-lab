# Royals Pressure Lab

An independent cricket analytics dashboard for the Rajasthan Royals **SupeRR Selector Season 2** challenge. Explore IPL player performance in demanding match situations, inspect the evidence behind the rankings, and compare conditional auction targets for IPL 2027.

**[Open the live website](https://royals-pressure-lab-swart.vercel.app)** · **[Read the methodology report](methodology-report.pdf)**

## What the dashboard includes

- Ordered batting and bowling rankings with sample sizes and 80% match-bootstrap intervals.
- Search, discipline and evidence filters, and CSV exports.
- Player profiles showing pressure-versus-ordinary performance and season history.
- Opportunity-based 2027 outlooks with historical-error ranges.
- Five batting and five bowling auction alternatives, analyst bid ceilings, and role-fit explanations.
- Retained squads, remaining purses and available squad/overseas slots for all ten teams, checked on **18 November 2026**.
- A downloadable six-page methodology report.

## Data coverage

| Purpose | Data |
| --- | --- |
| Ranked performance | Supplied IPL records from **2022–2026** |
| Scored sample | 357 eligible matches and 86,215 delivery events |
| 2022 contribution | 74 matches and 17,912 events |
| Initial historical baseline | Public Cricsheet IPL **2019–2021**, used for training only |
| Expectations for each season | The preceding three IPL seasons; no future seasons |

The supplied records were audited and three missing deliveries were reconciled against public IPL records. Matches with revised innings, no results or unresolved integrity exceptions were excluded. The final ranking is IPL-focused; supplied T20I performances are not pooled into it because a validated transfer adjustment is unavailable.

This repository publishes the website and derived summaries. It does **not** include the original competition data pack or the Python analysis pipeline. The PDF documents the analysis, but this repository alone cannot regenerate the ratings from raw deliveries.

## Method at a glance

1. Reconstruct the score, wickets, legal balls, required rate and innings phase **before** each delivery.
2. Identify tight/difficult chases, early collapses and first-innings finishes with depleted wickets using explicit rules documented in the PDF.
3. Compare runs and wickets with expectations for similar contexts, fitted using earlier seasons only. Sparse cells borrow evidence from phase averages; venue adjustments use prior scored seasons.
4. Calculate run-equivalent value using a 15-run wicket assumption and estimate player ability with small-sample shrinkage.
5. Select shrinkage and an additional pressure adjustment using 2024–2025 future-season errors. Report 2026 as a retrospective temporal diagnostic.
6. Jointly resample matches 400 times and rank by the lower 10th-percentile estimate.

Eligibility requires 180 total events, 60 pressure events, eight pressure matches and observed IPL participation in 2026. These are disclosed modelling choices.

**Key result:** both disciplines selected zero additional pressure weight in development testing. The published rankings therefore estimate general context-adjusted ability for pressure deployment. Observed pressure-versus-ordinary differences are shown separately and do not establish a repeatable standalone “clutch” skill.

## Interpreting auction recommendations

Performance rankings include retained players as benchmarks. The separate auction section considers released-player status, RR's roles, overseas slots and budget. Recommendations are **alternatives**, not ten simultaneous purchases. Release does not establish final auction registration, fitness or full-season availability. Bid ceilings are analyst budget limits, not predicted sale prices.

Availability and purse information are a dated snapshot and should be refreshed before an actual auction decision.

## Run locally

This is a static website with no framework, package installation, backend or API keys required.

```bash
git clone https://github.com/Harshit-OO7/royals-pressure-lab.git
cd royals-pressure-lab
python3 -m http.server 8080
```

Open **http://localhost:8080**. Use an HTTP server because the dashboard loads `data.json` with `fetch()`.

## Project structure

```text
index.html              Page structure and methodology
style.css               Main visual design
alignment.css           Responsive layout and form controls
app.js                  Filters, rankings, profiles and exports
data.json               Precomputed derived results and auction snapshot
rr-logo.png             Supplied Rajasthan Royals logo
methodology-report.pdf  Standalone submission report
vercel.json             Static deployment configuration
```

## Deploy on Vercel

Import this repository, select **Other** as the framework, use the repository root, and leave build/install commands empty. No environment variables are needed. The existing live deployment was uploaded directly; Git-based automatic deployment must be connected separately in Vercel.

## Validation and limitations

- Chronological model evaluation, shared match bootstraps and best-pressure-match removal diagnostics.
- Wicket-value sensitivity at 10 and 20 runs, plus annual context-residual checks.
- Website and PDF rankings checked for identical ordering.
- Forecasts assume delivery opportunities; they do not predict selection or injuries.
- Fixed wicket value, rule-based pressure, incomplete adjustment for era changes and no learned individual-opponent-strength model.
- Bootstrap intervals are conditional on fitted settings and omit model-selection uncertainty.
- Rankings are research estimates, not guarantees of IPL 2027 outcomes.

## Submission

The Round 1 brief asks for both ordered top-ten lists in Unstop's dropdowns and a methodology document. Pages 2–3 of the PDF contain the corresponding lists. Check the live submission form for accepted file types, limits and any player-pool restrictions. The auction shortlist is an additional decision layer.

## Sources and attribution

- Official SupeRR Selector competition data pack and Round 1 brief.
- [Cricsheet downloads](https://cricsheet.org/downloads/) and [licensing](https://cricsheet.org/licensing/).
- [Official IPL 2027 retention and purse announcement](https://www.iplt20.com/news/article/tata-ipl-2027-player-retentions-announced).
- [Official released-player list](https://www.iplt20.com/cms/files/jot2qw8s50z1/3gFAJ4z1USxcXYhaZVl65L/2a463a9c02a5bb7fd12fa3fbe91cc299/TATA_IPL_2027-_Release_Player_List.pdf).

Independent competition research; not an official Rajasthan Royals or IPL product. Team names, logos and third-party data remain subject to their owners' rights and applicable source terms. No blanket licence is granted for those assets by this repository.
