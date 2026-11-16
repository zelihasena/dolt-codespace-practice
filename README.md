# Dolt Codespace

A GitHub Codespace where an AI agent sets up [Dolt](https://www.dolthub.com),
a SQL database with Git-style versioning, and helps you clone, change, commit
and push a database you own on DoltHub.

## Before you start

1. Make an account on [DoltHub](https://www.dolthub.com) and stay signed in.
2. Click **Code → Codespaces → Create codespace on main** on this repo, and
   start your agent in the terminal.

## Exercises

Each folder is one exercise, with its own directions in a `README-` file:

| Folder | What you do |
|---|---|
| [make-your-own-database](make-your-own-database/README-make-your-own-database.md) | Pick a topic and the agent dreams up a small database about it: two tables joined by one foreign key. The agent first installs Dolt and logs you in to DoltHub, then you build it, query it, and push it to DoltHub. |
| [retail-orders](retail-orders/README-retail-orders.md) | The agent installs Dolt, logs you in to DoltHub, builds a retail orders database from `retail-orders.sql`, and pushes it to a new database on your DoltHub account. |
| [sales-csv-data](sales-csv-data/README-sales-csv-data.md) | Starting from one big `sales.csv` file, you and the agent design a database with three tables (stores, products and sales), build it in Dolt, and push it to DoltHub. |
| [excel-to-database](excel-to-database/README-excel-to-database.md) | Open an Excel workbook with two worksheets, find its problems, and with the agent turn it into a database whose keys keep those problems out. |
| [dolt-branches](dolt-branches/README-dolt-branches.md) | Build a small boutique database with three views, raise prices on a branch, compare what the views show on each branch, push the branch to DoltHub, and open a pull request for your manager to approve. |
| [company-analysis](company-analysis/README-company-analysis.md) | The agent analyzes an existing database, [calvinw/BusMgmtBenchmarks](https://www.dolthub.com/repositories/calvinw/BusMgmtBenchmarks), compares two retail companies in one year with charts, and builds a PowerPoint deck. |

Each exercise builds its database inside its own folder (for example
`retail-orders/retail-orders`). The `.gitignore` file keeps these databases
out of GitHub: you share them on DoltHub instead.

**Start with [make-your-own-database](make-your-own-database/README-make-your-own-database.md).**
Its Steps 1 to 4 install Dolt in your codespace and log you in to DoltHub;
the other exercises use that same setup. You can do the others in any order.
