<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=180&color=0:0E6B4C,100:12805C&text=SpendWise&fontColor=ffffff&fontSize=52&fontAlignY=42&animation=fadeIn" width="100%" alt="SpendWise banner" />

<img src="https://readme-typing-svg.demolab.com/?font=Manrope&weight=600&size=18&pause=1400&color=12805C&center=true&vCenter=true&width=560&lines=Track+income+and+expenses+in+seconds;See+your+budget+at+a+glance;Get+plain-language+spending+insights;Everything+stays+on+your+device" alt="Typing tagline" />

<br/>

![React](https://img.shields.io/badge/React-18.3-149ddb?logo=react&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-5.4-8B5CF6?logo=vite&logoColor=white)
![No backend](https://img.shields.io/badge/backend-none-12805C)
![Storage](https://img.shields.io/badge/storage-localStorage-12805C)
![License](https://img.shields.io/badge/license-MIT-5B6472)

</div>

<br/>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/screenshots/desktop-dark.png">
  <source media="(prefers-color-scheme: light)" srcset="docs/screenshots/desktop-light.png">
  <img alt="SpendWise dashboard" src="docs/screenshots/desktop-light.png" width="100%">
</picture>

<p align="center"><sub>This image follows your system's light / dark preference on GitHub — try toggling it. The app has the same switch built in.</sub></p>

<br/>

## Contents

- [See it in action](#see-it-in-action)
- [Features](#features)
- [Getting started](#getting-started)
- [Project structure](#project-structure)
- [How insights are generated](#how-insights-are-generated)
- [Design system](#design-system)
- [Data & privacy](#data--privacy)
- [FAQ](#faq)
- [License](#license)

<br/>

## See it in action

<div align="center">
  <img src="docs/screenshots/demo.gif" alt="Adding a transaction, switching categories, and toggling dark mode in SpendWise" width="720">
</div>

<sub>Recorded straight from the running app: opening the add-transaction modal, switching categories, and toggling dark mode.</sub>

<details>
<summary><strong>More screenshots</strong> — budget progress, category breakdown, mobile layout</summary>
<br/>

| Budget & category breakdown | Mobile dashboard |
| --- | --- |
| ![Budget progress and category donut chart](docs/screenshots/budget-donut.png) | <img src="docs/screenshots/mobile-light.png" width="260" alt="SpendWise on mobile"> |

**Auto-generated insights**

![Automatically generated spending insights](docs/screenshots/insights.png)

</details>

<br/>

## Features

<table>
<tr>
<td width="50%" valign="top">

**Track money in and out**
- Add, edit, and delete income & expense transactions
- Categories: Food, Transport, Education, Bills, Shopping, Other — plus Salary, Freelance, Investment for income
- Search transactions and filter by type or category

</td>
<td width="50%" valign="top">

**Understand where it goes**
- Dashboard: current balance, monthly income, monthly expenses, savings
- Monthly income-vs-expense chart, last 6 months
- Category breakdown donut for the current month

</td>
</tr>
<tr>
<td width="50%" valign="top">

**Stay on budget**
- Set a monthly budget
- Progress bar with over-budget warning
- Remaining / over-budget amount at a glance

</td>
<td width="50%" valign="top">

**Get a nudge, automatically**
- "Food is your highest spending category this month"
- "You've used 72% of your monthly budget"
- Month-over-month spend comparison and savings-rate callouts

</td>
</tr>
</table>

Also included: light/dark mode (follows system preference, toggle persists), a responsive layout with a collapsible mobile sidebar, subtle motion on load and interaction, and realistic seed data so the dashboard is never empty on first run.

<br/>

## Getting started

You'll need [Node.js](https://nodejs.org) 18 or later.

```bash
npm install     # install dependencies
npm run dev     # start the dev server, then open the printed localhost URL
```

Building for production:

```bash
npm run build     # outputs to dist/
npm run preview   # serve the production build locally
```

<br/>

## Project structure

<details>
<summary>Expand file tree</summary>

```text
src/
├─ components/          UI building blocks
│  ├─ Sidebar.jsx         Minimal nav + mobile drawer
│  ├─ TopBar.jsx          Page title, theme switch, add-transaction button
│  ├─ SummaryCards.jsx    Balance / income / expenses / savings cards
│  ├─ MonthlyChart.jsx    6-month income vs. expense bar chart (CSS only)
│  ├─ CategoryDonut.jsx   Current-month category breakdown (conic-gradient)
│  ├─ BudgetCard.jsx      Budget editing + progress bar
│  ├─ InsightsCard.jsx    Renders generated insights
│  ├─ TransactionsPanel.jsx  Search, filters, list
│  ├─ TransactionRow.jsx  Single row with edit/delete
│  ├─ TransactionModal.jsx  Add/edit form
│  ├─ ConfirmDialog.jsx   Delete confirmation
│  └─ icons.jsx           Inline SVG icon set (no icon library dependency)
├─ context/
│  └─ FinanceContext.jsx  App state, localStorage persistence, derived totals
├─ data/
│  └─ sampleData.js       Seed transactions, generated relative to today
├─ utils/
│  ├─ categories.js       Category list, colors, icon keys
│  ├─ helpers.js          Formatting & date utilities
│  └─ insights.js         Rule-based insight generator (pure function)
├─ App.jsx                Layout & section wiring
├─ index.css              Design tokens + all component styles
└─ main.jsx                Entry point
```

</details>

<br/>

## How insights are generated

Insights are produced by a small, pure rule set in `src/utils/insights.js` — no AI calls, just arithmetic on your own data, so results are instant and fully offline:

<details>
<summary>Expand the rules</summary>
<br/>

| Signal | Rule | Example |
| --- | --- | --- |
| Top category | Highest-spending category this month, flagged if it's ≥40% of total spend | *"Bills is your highest spending category this month, at $310.00 (38% of spending)."* |
| Budget usage | Percentage of monthly budget used, escalating tone past 80% and 100% | *"You've used 67% of your monthly budget."* |
| Month-over-month | Percent change in expenses vs. last month (shown if change ≥5%) | *"Spending is 12% lower than last month. Nice work."* |
| Savings rate | Share of income kept this month, praised above the 20% benchmark | *"You saved 83% of your income this month — ahead of the typical 20% target."* |

</details>

<br/>

## Design system

<details>
<summary>Expand tokens</summary>
<br/>

**Palette** — a warm neutral surface with a single emerald "growth" accent and a muted rose reserved only for spend:

![#12805C](https://img.shields.io/badge/Accent%20%2F%20Income-12805C?style=flat-square) ![#C1445E](https://img.shields.io/badge/Expense-C1445E?style=flat-square) ![#A9660F](https://img.shields.io/badge/Warning-A9660F?style=flat-square)

**Category colors:**

![#E0672E](https://img.shields.io/badge/Food-E0672E?style=flat-square) ![#3D74B6](https://img.shields.io/badge/Transport-3D74B6?style=flat-square) ![#7B5EA7](https://img.shields.io/badge/Education-7B5EA7?style=flat-square) ![#C1445E](https://img.shields.io/badge/Bills-C1445E?style=flat-square) ![#C79A1E](https://img.shields.io/badge/Shopping-C79A1E?style=flat-square) ![#5B6472](https://img.shields.io/badge/Other-5B6472?style=flat-square)

**Typography** — [Manrope](https://fonts.google.com/specimen/Manrope) throughout, with tabular figures (`font-variant-numeric: tabular-nums`) on every dollar amount so columns of numbers line up.

**Motion** — a single staggered rise-in on page load, a spring-like pop on modals, and smooth width/height transitions on bars and progress fills. Nothing animates on hover except a slight lift on summary cards; `prefers-reduced-motion` is respected everywhere.

**Charts** — the monthly chart and category donut are built with plain CSS (flex-sized bars and a `conic-gradient`), not a charting library, so there's one less dependency to install.

</details>

<br/>

## Data & privacy

Everything lives in your browser's `localStorage` — there is no server, no analytics, and no network request involved in storing your data:

| Key | Contents |
| --- | --- |
| `spendwise.transactions` | Your full transaction list |
| `spendwise.budget` | Your monthly budget amount |
| `spendwise.theme` | Your light/dark preference |

Clearing your browser storage, or opening the app in a different browser or device, resets it back to the sample data.

<br/>

## FAQ

<details>
<summary>Can I use my own currency?</summary>
<br/>
Amounts are formatted as USD by default. Change the <code>Intl.NumberFormat</code> options in <code>src/utils/helpers.js</code> (<code>formatCurrency</code>) to switch currency or locale.
</details>

<details>
<summary>How do I reset the app back to sample data?</summary>
<br/>
Open your browser's dev tools → Application → Local Storage, and delete the three <code>spendwise.*</code> keys for this site, then refresh.
</details>

<details>
<summary>Can I add my own categories?</summary>
<br/>
Yes — edit the <code>EXPENSE_CATEGORIES</code> / <code>INCOME_CATEGORIES</code> arrays in <code>src/utils/categories.js</code>. Each entry just needs an id, label, color, and an icon key from <code>src/components/icons.jsx</code>.
</details>

<details>
<summary>Is there a backend I can connect this to later?</summary>
<br/>
Not out of the box. All reads/writes go through <code>FinanceContext</code> in <code>src/context/FinanceContext.jsx</code>, so swapping <code>localStorage</code> for an API is mostly a matter of replacing the functions in that one file.
</details>

<br/>

## License

MIT — do whatever you'd like with it.

<div align="center">
<sub>Built with React + Vite. No backend, no tracking, no accounts.</sub>
</div>
