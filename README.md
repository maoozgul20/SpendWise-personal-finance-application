# SpendWise

A polished, single-user personal finance dashboard built with React and Vite. Track income and expenses, set a monthly budget, and get automatic plain-language insights about your spending — all stored locally in your browser, with no backend and no account required.

## Features

- **Add, edit and delete transactions** — income or expense, with category, amount, description and date
- **Categories** — Food, Transport, Education, Bills, Shopping, Other for expenses; Salary, Freelance, Investment, Other Income for income
- **Dashboard** with current balance, monthly income, monthly expenses and savings
- **Transaction history** with live search and category/type filtering
- **Monthly spending chart** comparing income vs. expenses over the last 6 months
- **Category breakdown** donut chart for the current month
- **Monthly budget** with a progress bar and remaining/over-budget status
- **Automatic insights**, e.g. "Food is your highest spending category this month" or "You've used 72% of your monthly budget"
- **Light and dark mode**, following your system preference by default
- **Responsive design** — a collapsible sidebar drawer on mobile, full sidebar on desktop
- **Realistic sample data** pre-loaded on first run so the dashboard isn't empty
- **Everything persists in `localStorage`** — refresh the page and your data is still there

## Getting started

You'll need [Node.js](https://nodejs.org) 18 or later installed.

```bash
# Install dependencies
npm install

# Start the dev server
npm run dev
```

Then open the URL Vite prints (usually `http://localhost:5173`).

To build a production bundle:

```bash
npm run build
npm run preview   # optional: preview the production build locally
```

## Project structure

```
src/
  components/        UI building blocks (cards, charts, modals, sidebar, etc.)
  context/            FinanceContext — app state, localStorage persistence, derived totals
  data/sampleData.js   Seed transactions shown on first launch
  utils/              Formatting helpers, category config, insight-generation rules
  App.jsx              Page layout and section wiring
  index.css            Design tokens and all component styles (light + dark themes)
```

## How data is stored

Three keys are used in `localStorage`:

- `spendwise.transactions` — the full transaction list
- `spendwise.budget` — your monthly budget amount
- `spendwise.theme` — your light/dark preference

There is no server and no network request involved in storing your data — it lives only in this browser. Clearing your browser storage (or using a different browser/device) will reset the app back to the sample data.

## Notes on the sample data

The seed transactions in `src/data/sampleData.js` are generated relative to today's date, so the monthly chart and insights always have a few months of realistic history no matter when you first run the app. Feel free to delete them from the Transaction history panel once you've explored the app, or clear `localStorage` for a completely blank slate.
