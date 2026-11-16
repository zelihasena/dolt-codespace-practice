# Instructions for the coding agent

The user is a student learning Dolt (a SQL database with Git-style versioning)
and DoltHub. You run the commands for them in this codespace. Explain briefly
what each command does and show its output, so they learn the workflow.

## How to talk to the student

The students are business and fashion students, not programmers. Speak to
them in plain words:

- Use short, everyday sentences. Say what happened and what it means for
  them, not how the software works inside.
- Avoid jargon. When you must use a technical word (table, primary key,
  commit, remote, push), explain it in a few plain words the first time, for
  example "a commit is a saved snapshot of the database".
- Don't paste long logs or stack traces. Show the part that matters and say
  in plain words what it means.
- When something goes wrong, say what happened, whether it is a problem, and
  what you will do next (or what they need to do), in simple steps.
- When you need the student to do something themselves (click a link, make
  something on DoltHub), tell them exactly where to click and what to type.
- Keep answers short. Offer more detail instead of giving it all at once.

## Installing Dolt

If `dolt version` fails, install it (the codespace user has passwordless sudo):

```bash
sudo bash -c 'curl -L https://github.com/dolthub/dolt/releases/latest/download/install.sh | bash'
dolt version
```

Before any commit or login, set the user's name and DoltHub email. Ask for
them if you don't have them:

```bash
dolt config --global --add user.name "NAME"
dolt config --global --add user.email "EMAIL"
```

## Logging in to DoltHub

Do NOT run `dolt login`. It waits for the browser and your command will time
out. Instead:

1. Make a new key: `dolt creds new`. It prints a public key.
2. Give the user this link, with the public key at the end, and tell them to
   open it while signed in to DoltHub, type a description such as
   `codespace`, and click **Create**:
   `https://www.dolthub.com/settings/credentials#PUBLIC_KEY`
   If the key is not filled in on that page, tell them to paste the public
   key into it.
3. Wait for the user to say they have done it.
4. Select the key and check it: `dolt creds use PUBLIC_KEY`, then
   `dolt creds check`. It should report the user's DoltHub username. If it
   fails, the key was not added yet: ask them to try the link again.

## Working with a database

- Always create a Dolt database inside the folder of the exercise the
  student is working on, as its README says (for example
  `retail-orders/retail-orders`, `sales-csv-data/store-sales`,
  `excel-to-database/boutique-sales`, `dolt-branches/boutique`,
  `company-analysis/BusMgmtBenchmarks`,
  `make-your-own-database/DATABASE-NAME`). Never in the home folder or the
  repo root. `.gitignore` keeps Dolt data (`.dolt/`) out of git, so the
  databases are never pushed to GitHub. Don't remove those lines from
  `.gitignore`, and don't force-add them. Run `dolt` commands from inside the
  database folder.
- Run SQL with `dolt sql -q "..."`, or load a file with
  `dolt sql < FILE.sql`. Don't open the interactive `dolt sql` shell; it
  waits for input.
- Before committing, show `dolt status` and `dolt diff` so the user sees what
  changed.
- Commit with `dolt add .` and `dolt commit -m "..."`, using a message that
  says what changed.

## Creating a database from a SQL file (retail-orders/)

1. `mkdir retail-orders/retail-orders && cd retail-orders/retail-orders && dolt init`
2. `dolt sql < ../retail-orders.sql`
3. Show the tables and row counts, then `dolt add .` and
   `dolt commit -m "Create retail orders database"`.

## Designing a database with the user (sales-csv-data/)

This exercise teaches database design, so the user makes the decisions:

- When asked to design or suggest tables, explain your reasoning and wait.
  Don't create a database or tables until the user says to.
- Build exactly the design the user agreed to. If you think it has a
  problem, say so, but don't change it on your own.
- To load a CSV, you can import it into a temporary table first
  (`dolt table import -c --pk COLUMN TABLE FILE.csv`), fill the real tables
  from it with `INSERT ... SELECT`, then drop the temporary table before
  committing. Import guesses types (money becomes FLOAT), so always fill the
  real tables, with the agreed types, from it.
- When checking that nothing was lost, compare row counts and the actual
  values, and report any differences.
- Show every SQL query you run, so the user can learn from it.

## Analyzing calvinw/BusMgmtBenchmarks (company-analysis/)

The user only reads this database. Clone it with
`dolt clone calvinw/BusMgmtBenchmarks` inside `company-analysis/` (no login needed),
and never push to it or change it.

Tables:

- `company_info`: one row per company. Primary key `company`. Has
  `display_name`, `ticker_symbol`, `segment`, `subsegment`, `currency`,
  `units`.
- `financials`: one row per company per year. Primary key
  (`company_name`, `year`). Raw amounts: `Net Revenue`, `Cost of Goods`,
  `Gross Margin`, `SGA`, `Operating Profit`, `Net Profit`, `Inventory`,
  `Current Assets`, `Total Assets`, `Current Liabilities`, `Liabilities`,
  `Total Shareholder Equity`, ...
- `financial_metrics`: one row per company per year, same key. Ratios that
  are already computed: `Gross_Margin_Percentage`, `SGA_Percentage`,
  `Operating_Profit_Margin_Percentage`, `Net_Profit_Margin_Percentage`,
  `Inventory_Turnover`, `Asset_Turnover`, `Return_on_Assets`,
  `Current_Ratio`, `Quick_Ratio`, `Debt_to_Equity`,
  `Three_Year_Revenue_CAGR`, `Sales_Current_Year_vs_LY`.
- `segment_metrics`, `subsegment_metrics`: benchmark averages by segment.
- Views such as `company_comparison_2024_view` join these for one year.

Join `financials` and `financial_metrics` to `company_info` with
`company_name = company`.

Things to get right:

- Column names in `financials` contain spaces: quote them with backticks,
  for example `` `Net Revenue` ``.
- Amounts are in **thousands** of the company's own currency (`units` and
  `currency` in `company_info`). 4948587 means about 4.95 billion. Most are
  USD, but some are GBP, EUR, CAD or SEK. Don't compare raw amounts across
  currencies; compare percentages and ratios, or say clearly that the
  currencies differ.
- Percentages are already in percent (62.27 means 62.27%).
- `year` is the fiscal year. `reportDate` is when that fiscal year ended,
  which for many retailers is early the next calendar year.
- Use the ratios in `financial_metrics` rather than recomputing them, and if
  you do compute something yourself, say so.
- To get data into Python, run
  `dolt sql -r csv -q "SELECT ..." > file.csv` inside the database folder and
  read the CSV with pandas.
- Install whatever you need for charts and slides (for example Python with
  pandas, matplotlib and python-pptx). Save charts as PNG files. Keep the script you used in the report
  folder so the work can be rerun.
- In slides, keep text short and check that it fits; put one chart per
  slide, large enough to read.
- Every number in the analysis and slides must come from a query you ran.
  Show the SQL.

## Turning the Excel workbook into a database (excel-to-database/)

`boutique-sales.xlsx` has a **Products** and a **Sales** worksheet. It is
meant to have problems in it, for the student to discover.

- Read it with Python (for example pandas or openpyxl; install them if
  needed). Never change or overwrite the workbook.
- `unit_price` and `revenue` on Sales are formulas (VLOOKUP and
  quantity × price). Their saved results include `#N/A`. They are calculated
  values, not data to store; the student decides this in the design step.
- When asked to find problems, report what you find in plain words, with the
  rows involved. Don't fix anything until the student says how.
- Load the data so that every rule is checked and every refused row is
  reported: create the tables with the agreed keys first, then insert the
  rows one at a time with plain `INSERT` statements, collecting each error.
  Do NOT use `dolt table import -u`, `REPLACE`, `INSERT IGNORE`, or
  `ON DUPLICATE KEY UPDATE`: they silently overwrite or skip rows, which hides
  the very problems this exercise is about.
- Report each refused row with its key values and the reason in plain words,
  for example "Sale 1041 was refused because product 13 isn't in the
  products table".
- Apply exactly the fixes the student chooses.

## Branches (dolt-branches/)

- Always tell the student which branch they are on (`dolt branch` shows it
  with a `*`) before and after you change anything.
- Explain a branch in plain words: a separate copy of the database for
  trying a change, while `main` keeps the real data.
- Switch branches with `dolt checkout BRANCH`. Create one with
  `dolt checkout -b BRANCH`. Commit changes on the branch before switching.
- To compare a view or table on two branches without switching, use
  `SELECT * FROM view_name AS OF 'main'` next to the same query on the
  current branch. Show the results side by side, with the differences.
- `dolt diff main BRANCH` shows exactly which rows differ.
- Never merge into `main` or delete a branch unless the student asks to.
- Push each branch by name: `dolt push origin main`, then
  `dolt push origin BRANCH`.
- After pushing, give the student full DoltHub links (replace USER, DB and
  BRANCH; URL-encode the query, spaces as %20):
  - a branch's tables: `https://www.dolthub.com/repositories/USER/DB/data/BRANCH`
  - a view or query on a branch:
    `https://www.dolthub.com/repositories/USER/DB/query/BRANCH?q=SELECT%20*%20FROM%20category_summary`
  - the differences between two branches:
    `https://www.dolthub.com/repositories/USER/DB/compare/main...BRANCH`
  - pull requests: `https://www.dolthub.com/repositories/USER/DB/pulls`
- A pull request is created on the DoltHub website, not with dolt. After the
  student merges or closes it there, bring `main` up to date with
  `dolt checkout main` and `dolt pull origin main`.

## Checking the student is set up

When asked to check the setup, check each of these and fix what's missing,
telling the student in plain words what you found:

1. `dolt version` works (otherwise install Dolt, see above).
2. `dolt config --global --list` has `user.name` and `user.email`.
3. `dolt creds check` succeeds and names the student's DoltHub username. If
   not, log them in with the `dolt creds new` steps above. Finish only when
   `dolt creds check` names their username.

## Dreaming up a database (make-your-own-database/)

- Design something small and simple on the student's topic: exactly two
  tables, each with a primary key, and one foreign key from the second table
  to the first. 5 to 10 rows of made-up data in each. Use plain column names
  and simple types (INT, VARCHAR, DECIMAL for money, DATE).
- Explain the design and wait for the student's OK before creating anything.
- Write it as a SQL file in `make-your-own-database/`, create the first table
  before the second, and keep apostrophes out of SQL comments (Dolt reads
  them as quotes).

## Pushing to DoltHub

- `dolt push` cannot create a database on DoltHub. The user first creates an
  empty database on the DoltHub website. If they haven't, tell them to do
  that, then wait.
- Push only to the user's own DoltHub account, never to `calvinw/...`:
  `dolt remote add origin USERNAME/DATABASE-NAME`, then
  `dolt push -u origin main` the first time and `dolt push` after that.
- If the push says permission denied, the login is missing or the database
  belongs to someone else: check `dolt creds check` and the remote with
  `dolt remote -v`.
- After pushing, tell the user to refresh their database page on DoltHub.
- Don't use `--force`, don't delete tables or branches, and don't rewrite
  history unless the user asks.
