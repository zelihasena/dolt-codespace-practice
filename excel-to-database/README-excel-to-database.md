# From an Excel Workbook to a Database

`boutique-sales.xlsx` is how a small fashion boutique keeps its records: a
workbook with two worksheets.

| Worksheet | What it holds |
|---|---|
| **Products** | The product list from the buying team: `product_id`, `product_name`, `category`, `color`, `cost` (what the boutique pays) and `price` (what the customer pays) |
| **Sales** | Every sale from the registers, January to June 2026: `sale_id`, `sale_date`, `store`, `product_id`, `quantity`, plus two formula columns. `unit_price` looks up the price on the Products sheet with `VLOOKUP`, and `revenue` is `quantity × unit_price` |

The workbook has **two problems** hidden in it. They are the kind of mistakes
that creep into real spreadsheets. In this exercise you find them, then you and
the agent turn the workbook into a database that **won't let these mistakes
in**, and you see what else a database does better than a spreadsheet.

## Step 1: Look at the Workbook Yourself

1. In the codespace's file list on the left, open the `excel-to-database`
   folder. Right-click `boutique-sales.xlsx` and choose **Download**.
2. Open it in **Excel**, or in **Google Sheets** (go to
   <https://sheets.google.com>, then **File → Import → Upload**).
3. Look at both worksheets (the tabs at the bottom). Scroll through them.

Write down anything that looks wrong or odd. Hints: look closely at the
`unit_price` and `revenue` columns on **Sales**, and compare the rows on
**Products** with each other.

## Step 2: Have the Agent Check the Workbook

Start your agent in the terminal. Copy each prompt into the agent and press
**Enter**. Read what the agent says before you go on. If it asks to install
something, allow it.

```default
Look at excel-to-database/boutique-sales.xlsx. Describe its two worksheets: what one row means on each, and how the sheets are connected. Then find anything wrong with the data that would cause problems, and explain each problem in plain words. Don't change the file.
```

Did the agent find the same problems you did? Did it find one you missed?

```default
For each problem you found: how would it affect the total revenue someone calculates in this workbook? Would someone looking only at the totals notice it?
```

## Step 3: Design the Database

```default
I want to turn this workbook into a Dolt database with two tables, products and sales. Don't create anything yet. Suggest the columns of each table, a data type for each column, the primary key of each table, and the foreign key that connects them. Should unit_price and revenue be stored in the sales table? Explain why or why not.
```

Read the design. Make sure you understand:

- what the **primary key** of `products` is, and which problem it prevents;
- what the **foreign key** in `sales` is, and which problem it prevents.

Ask the agent about anything you don't understand. When you are happy with
the design, go on.

## Step 4: Build It and Watch the Database Say No

If Dolt isn't set up yet in this codespace, or you aren't logged in to
DoltHub, do Steps 1 to 4 of the
[make-your-own-database](../make-your-own-database/README-make-your-own-database.md) exercise before you go on.

```default
Create a new Dolt database in a folder called excel-to-database/boutique-sales. Create the two tables exactly as we designed them. Then load every row from both worksheets of the workbook, and tell me about every row the database refuses and why. Don't fix anything yet.
```

The database should refuse some rows. Each refusal is one of the problems
from Step 1, caught by a rule you designed.

## Step 5: Decide the Fixes

The database tells you **something** is wrong. Deciding **what is right** is
a business decision, so it's yours, not the agent's. For each problem, choose
a fix and tell the agent. For example:

- If a product appears twice with two different prices, which price is
  correct?
- If some sales are for a product that isn't on the product list, is it a
  real product that is missing from the list (then add it, with a name,
  category, color, cost and price), or a typo for a different product?

```default
Here is how I want to fix the problems: (DESCRIBE YOUR FIXES). Make those fixes, load the rows that were refused, and show me how many rows each table has now. Then check that every sale points to a product.
```

```default
Commit the database with a message that says what it contains and how the problems were fixed.
```

## Step 6: Use the Database

```default
What was the total revenue and the total profit (price minus cost, times quantity) for each store? Show me the SQL you used.
```

```default
What was the revenue for each category in each month? Show me the SQL you used.
```

Now change a price, the way a store does when it raises prices:

```default
Raise the price of the Silk Scarf by $4. Then show me the revenue for each category again. Show me exactly what changed in the database, and commit it with a clear message.
```

Think about the same change in the workbook: where would you have to change
the price, and what could go wrong?

## Step 7: Push to DoltHub

On DoltHub, go to <https://www.dolthub.com/profile> and click
**Create Database**. Name it `boutique-sales`, make it **Public**, and click
**Create**. Leave it empty.

```default
Add my DoltHub database YOUR-DOLTHUB-USERNAME/boutique-sales as the remote called origin and push main to it.
```

Refresh the page on DoltHub and open the **Commit Log** to see your commits.

## What to Hand In

1. The link to your `boutique-sales` database on DoltHub.
2. Short answers, in your own words:
   - What were the two problems in the workbook, and which one was harder to
     notice in Excel or Google Sheets? Why?
   - Which database rule caught each problem?
   - How did you fix each one, and why?
   - Name three things the database did better than the workbook.
