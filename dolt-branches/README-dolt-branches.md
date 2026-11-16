# Try a Price Increase on a Branch

A boutique's manager wants to know: **what if we raised prices?** In a
spreadsheet you would copy the file (`prices_v2_FINAL.xlsx`) and hope nobody
mixes up the copies. In Dolt you make a **branch**: a separate copy of the
database where you can try a change without touching the real data, which
stays on the branch called `main`.

`boutique.sql` builds a small boutique database:

| Name | What it is |
|---|---|
| `products` (table) | 12 products, with `cost` (what the boutique pays) and `price` (what the customer pays) |
| `sales` (table) | 200 sales from January to March 2026: date, store, product and quantity |
| `category_summary` (view) | Units sold, revenue and profit for each category |
| `store_summary` (view) | Number of sales, revenue and profit for each store |
| `product_margins` (view) | Each product's cost, price, margin %, units sold and revenue |

A **view** is a saved query. It doesn't store numbers; it calculates them
from the tables every time you look at it. So the same view shows different
numbers on different branches.

## Before you start

1. Start your agent in the terminal.
2. If Dolt isn't installed in this codespace yet, or you aren't logged in to
   DoltHub, do Steps 1 to 4 of the
   [make-your-own-database](../make-your-own-database/README-make-your-own-database.md) exercise first. (You need the login for Step 7.)

Copy each prompt into the agent and press **Enter**. Read what the agent says
before you go on.

## Step 1: Build the Database

```default
Create a new Dolt database in a folder called dolt-branches/boutique. Load dolt-branches/boutique.sql into it, show me its tables and views, and commit it with the message "Create boutique database with three views".
```

## Step 2: Look at the Views on main

```default
Explain each of the three views in plain words. Then show me what each one shows right now, on the main branch.
```

Write down the total revenue and profit for each category. You will compare
them later.

## Step 3: Make a Branch

Pick one category (Dresses, Tops, Bottoms, Outerwear or Accessories) and a
price increase, for example 10%.

```default
Explain what a branch is. Then create a branch called price-increase and switch to it. Tell me which branch I am on.
```

## Step 4: Raise the Prices on the Branch

```default
On the price-increase branch, raise the price of every CATEGORY product by PERCENT. Show me exactly which rows changed, then commit it with a message that says what you changed.
```

## Step 5: Compare the Views

```default
Show me each of the three views on main and on price-increase, side by side, with the difference. Which numbers changed, which stayed the same, and why?
```

Think about it:

- Why did revenue go up but **units sold** stay the same?
- Which stores gained the most, and why those?
- What happened to the margin % of the products whose price went up?
- The views assume customers buy the same amount at the higher price. Is
  that realistic? What might really happen?

## Step 6: See Exactly What Changed

```default
Show me everything that is different between main and price-increase, and the commit history of each branch.
```

Notice that only a few rows in `products` changed, yet every report that uses
prices changed with them. In a workbook, you would have to make sure every
sheet and formula picked up the new prices.

## Step 7: Put Your Branch on DoltHub for Your Manager

Your manager can't see your codespace, so put the database on DoltHub, with
**both** branches.

On DoltHub, go to <https://www.dolthub.com/profile> and click
**Create Database**. Name it `boutique-branches`, make it **Public**, and
click **Create**. Leave it empty.

If you haven't logged in to DoltHub in this codespace yet, do Steps 3 and 4
of the [make-your-own-database](../make-your-own-database/README-make-your-own-database.md) exercise first.

```default
Add my DoltHub database YOUR-DOLTHUB-USERNAME/boutique-branches as the remote called origin, and push both the main and the price-increase branches to it. Then give me the DoltHub links where my manager can see: the price-increase branch, each of the three views on price-increase, the same views on main, and the differences between main and price-increase.
```

Open each link the agent gives you. On DoltHub you can also use the
**branch** menu (it says `main`) to switch between `main` and
`price-increase`.

## Step 8: Ask Your Manager to Approve It

On DoltHub, a **pull request** is how you ask someone to review a branch and
bring it into `main`.

1. On your `boutique-branches` page, click **Pull Requests**, then
   **Create Pull Request**.
2. Set it to merge **from** `price-increase` **into** `main`.
3. Give it a title such as "Raise Dresses prices 10%". In the description,
   write two or three sentences for your manager: what you changed, and what
   happens to revenue and profit (use your numbers from Step 5).
4. Click **Create Pull Request**. Open its **Diff** tab to see what your
   manager will see.

Copy the link to your pull request.

## Step 9: Decide

Now be the manager. Read the pull request and decide:

- **Approve:** click **Merge**. The new prices become part of `main`.
- **Reject:** click **Close**. `main` keeps the old prices, and the branch
  stays as a record of the idea.

```default
Get the latest main branch from DoltHub, then show me the category_summary view on main and the commit history of main. Did the price increase become part of main?
```

## What to Hand In

1. The link to your pull request on DoltHub.
2. Short answers, in your own words:
   - Which category did you change, and by how much?
   - How did revenue and profit change for that category, and for the whole
     business?
   - Did you merge the pull request or close it? Why?
   - Why is a branch safer than editing the real data, or copying a
     spreadsheet?
