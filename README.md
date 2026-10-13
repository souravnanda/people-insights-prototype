# People Insights: retention and collaboration prototype

**Live demo:** https://YOUR-USERNAME.github.io/people-insights-prototype/

A clickable prototype of two people-analytics dashboards. It is designed to help HR business partners act on retention and workload risks early, and to protect employee privacy by design.

> All data in this prototype is synthetic. It does not use or represent any real company's data.

## The problem

- **Exit interviews come too late.** By the time someone resigns, there is no chance to act. People also rarely give the real reason on the way out.
- **Org charts show reporting lines, not how work flows.** Collaboration bottlenecks and overloaded teams stay hidden until people burn out or leave.

## The two dashboards

### 1. Retention Radar (`index.html`)
An early warning for **teams, not individuals**.
- Leaving risk by team and experience tier, with the drivers behind it: manager change, slow promotion, pay below band, workload, a lack of recognition, and feedback sentiment.
- **Regretted attrition exposure:** the share of top-rated people in each at-risk group, and the estimated cost of replacing them.
- Suggested actions for HR business partners, plus a "did the actions work?" comparison against similar groups that got no action.

### 2. Collaboration and Load (`collaboration.html`)
How work actually flows between teams.
- A team network map that highlights fragile links: work between two teams that runs through 2 or fewer people.
- Workload by team (meeting hours, after-hours messages, focus time), and a load vs. results 2x2.
- Cross-team recognition, with **anti-gaming rules** for kudos:
  - Repeated pairs count for less over time.
  - Mutual "swaps" count once.
  - Generic notes count for less.
  - Each giver has a weekly cap.
  - Rings of people who mostly thank each other are flagged for review.

## Key design decisions

| Decision | Why |
|---|---|
| Team-level only, with groups under 5 hidden | Individual "flight-risk" scores erode trust and can change how managers treat people |
| No message content, only timing and team | Metadata is enough to see load and flow, and content would be surveillance |
| Individual ratings stay in the performance system | Only team totals are used, to tie risk to business cost |
| Hidden connectors are counted, not named, unless they opt in | Recognition should be offered, not imposed |
| Kudos never feed pay or bonuses | Once a number decides pay, people optimize the number (Goodhart's law) |
| A person makes every decision | The dashboards suggest actions and never act on their own |

## Data sources (in a real build)

| Data | Source system | Refresh |
|---|---|---|
| Reporting lines, job and level history, voluntary exits | HR information system (HRIS) | Daily |
| Pay vs. band | Compensation system plus market pay bands | Each pay cycle |
| Top-rated share (team totals only) | Performance system | Each review cycle |
| Kudos and awards | Recognition platform | Daily |
| Feedback themes and sentiment | Pulse surveys, feedback tool, public internal channels | Weekly |
| Meeting and message timing | Calendar, email and chat metadata (no content) | Weekly |
| Team goal attainment | Goal tracker (team goals only) | Quarterly |

Data would be loaded by ETL into a people data warehouse. The dashboards read team-level tables where small groups are already removed. Free text is summarized into themes with generative AI, and each theme links back to its source comments.

## What I would build next

1. A data model and SQL for each metric, with one agreed definition per metric.
2. A pilot with one HR business partner group, measuring whether suggested actions get taken and whether risk falls.
3. A bias and privacy review before any real data is connected.

## How to view

Open `index.html` in a browser, or use the live demo link above. Navigation at the top switches between the two dashboards.
