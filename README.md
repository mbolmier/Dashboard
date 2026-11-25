# Management dashboards for a network of racket-sport clubs

Three interactive dashboards I designed during my Data Analyst internship at ALL IN GROUP (2026), for a network of padel, tennis, badminton and pickleball clubs. Each one answers a specific management question and can be read in a few seconds: key figures at the top, compared with the previous period, then the details in charts.

**All data is fictitious.** Customer names and figures are made up: series written in the code or produced by a fixed-seed pseudo-random generator. No real data is published.

**Live demo: https://mbolmier.github.io/Dashboard/**

![Preview of the court occupancy dashboard](docs/occupation.png)

## Live demo

| Dashboard | The question it answers | Link |
|---|---|---|
| Court occupancy | Which courts, days and hours are full or empty? | [Open](https://mbolmier.github.io/Dashboard/Taux%20d'occupation%20des%20terrains.html) |
| Customers & loyalty | How many customers are active, who is moving up, who is dropping off? | [Open](https://mbolmier.github.io/Dashboard/client.html) |
| Customer wallets | How much prepaid money is in circulation, and how is it topped up and spent? | [Open](https://mbolmier.github.io/Dashboard/wallets.html) |

The dashboards' interface is in French, like the company they were built for.

## What each dashboard shows

### 1. Court occupancy

- **Filters**: period (7 days, 1, 3 or 6 months, 1 year, or custom dates), sport, activity type (tournaments, events, lessons, free play).
- **Key figures**: overall occupancy rate and booked slots, with their change from the previous period; least active day; hours booked.
- **Charts**: monthly occupancy trend (with the previous period for comparison), average occupancy by day of the week, court ranking, hours blocked by tournaments, lessons and events, and an hour × day heatmap to spot empty slots.

### 2. Customers & loyalty

- **Key figures**: total customers, active customers over a rolling 3-month window, new customers, average frequency.
- **Segmentation by playing frequency** over 3 months: Rookie (1 game), Specialist (2 to 3), Elite (4 to 5), Legend (6 or more), with how each segment evolves and how many customers moved up a segment.
- **Flows**: new customers versus newly inactive ones, to see whether the base is growing or shrinking.
- **Revenue by category** (sports, restaurant, rentals, memberships), weekday / weekend playing habits, and the top 50 most active customers.

### 3. Customer wallets

- **Snapshot at a given date**: total balance in circulation, active wallets, distribution of wallets by balance range (active and inactive).
- **Over a period**: top-ups, spending and spending breakdown by category.
- **Monthly history per customer**: end-of-month balance and bonuses credited.

## How it works

- **One self-contained HTML file per dashboard** (HTML, CSS, JavaScript), with no framework and no build step: just open it in a browser.
- **Chart.js 4**, loaded from a CDN, draws the bar and line charts. The heatmap and tables are built directly in JavaScript.
- **Data generated in the browser**: a fixed-seed pseudo-random generator (`seededRand`, a linear congruential generator) produces reproducible series, so the same period always shows the same figures.
- **A single refresh point**: every filter change calls `refreshAll()`, which recomputes the key figures and the change badges against the previous period, then redraws the charts.
- **Layout adapted to narrower screens** (media queries) and **published with GitHub Pages**.

## Run it locally

```bash
git clone https://github.com/mbolmier/Dashboard.git
cd Dashboard
python3 -m http.server 8000
```

Then open http://localhost:8000. Opening one of the HTML files directly in the browser also works.

## Limitations

These are design prototypes: the data is fictitious and the "Exporter" (export) button is not wired up yet. To go to production, the generated series would be replaced by an automatically refreshed export of bookings and sales.

---

Martin Bolmier, Data Science student (BUT Science des données, Lyon) · [LinkedIn](https://www.linkedin.com/in/martin-bolmier-501b92301/)
