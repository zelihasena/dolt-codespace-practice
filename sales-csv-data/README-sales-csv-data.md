# Design a Store Sales Database with an Agent

`sales.csv` is an export of two months of sales (March and April 2026) from a
fashion boutique with three stores. It is one big table: 60 rows, one row for
each sale.

| Column | What it means |
|---|---|
| `sale_id` | A number that identifies the sale |
| `sale_date` | The day of the sale |
| `store_id`, `store_name`, `city`, `opened_date` | The store where the sale happened, and when that store opened |
| `product_id`, `product_name`, `category`, `color` | The product that was sold |
| `cost` | What the boutique pays the supplier for one item |
| `price` | What the customer pays for one item |
| `quantity` | How many items were sold in this sale |

Storing everything in one table repeats a lot of information. Your job is to
work with the agent to **design** a better database with three tables,
**create** it in Dolt, and **push** it to DoltHub. The agent does the typing.
You make the decisions, so read its answers and push back when something
doesn't make sense.

## Before you start

1. Start your agent in the terminal.
2. If Dolt isn't installed in this codespace yet, or you aren't logged in to
   DoltHub, do Steps 1 to 4 of the
   [make-your-own-database](../make-your-own-database/README-make-your-own-database.md) exercise first.

Copy each prompt into the agent and press **Enter**. Read what the agent says
before you go on. Replace the parts in capitals with your own details.

## Step 1: Understand the Data

```default
Look at sales-csv-data/sales.csv. Tell me what one row represents, and show me examples of information that repeats from row to row.
```

```default
If the Williamsburg store moved to a new city, how many rows of sales.csv would I have to change? What could go wrong if I missed one?
```

## Step 2: Design the Tables

```default
I want to split this data into three tables: stores, products and sales. Don't create anything yet. Suggest which columns belong in each table, the primary key of each table, the foreign keys that connect them, and a data type for every column. Explain why each column goes where it goes.
```

Now check the design yourself before you build it. Ask the agent about
anything you don't understand. Some questions to think about (ask the agent
if you're stuck):

- Two products are both called "Linen Wrap Dress". Why can't the product
  name be the primary key of `products`?
- Should `price` go in `products` or in `sales`? What would change if prices
  went up next month?
- Why should money columns be `DECIMAL` and not `FLOAT`?

If you want to change something, tell the agent. For example:

```default
Add a NOT NULL to every column that should always have a value. Show me the final design as CREATE TABLE statements, but don't run them yet.
```

## Step 3: Create the Database

When you are happy with the design:

```default
Create a new Dolt database in a folder called sales-csv-data/store-sales. Create the three tables exactly as we designed them, fill them with all the data from sales-csv-data/sales.csv, and show me how many rows each table has.
```

```default
Check that nothing was lost: join the three tables back together and confirm that every row of sales.csv comes back with the same values.
```

```default
Commit the database with the message "Create store sales database from sales.csv".
```

## Step 4: Push to DoltHub

On DoltHub, go to <https://www.dolthub.com/profile> and click
**Create Database**. Name it `store-sales`, make it **Public**, and click
**Create**. Leave it empty.

```default
Add my DoltHub database YOUR-DOLTHUB-USERNAME/store-sales as the remote called origin and push main to it.
```

Refresh the page on DoltHub. You should see your three tables.

## Step 5: Use the Database

Ask the agent to answer these with SQL that joins your tables. Have it show
you the query each time.

```default
What was the total revenue (price times quantity) for each store? Sort from highest to lowest.
```

```default
What was the profit (price minus cost, times quantity) for each category?
```

```default
Which product sold the most items at each store?
```

Then ask at least two questions of your own.

## What to Hand In

1. The link to your `store-sales` database on DoltHub.
2. Short answers to the three questions in Step 2, in your own words.
