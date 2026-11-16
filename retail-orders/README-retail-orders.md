# Create the Retail Orders Database with an Agent

In this exercise an agent builds a Dolt database on your codespace from the
SQL file in this folder, commits it, and pushes it to a new database on your
DoltHub account. Then you change it and push again.

`retail-orders.sql` creates three tables and fills them with data:

| Table | What it holds |
|---|---|
| `customers` | 8 customers: `customer_id`, `first_name`, `last_name`, `email` |
| `products` | 10 products: `product_id`, `name`, `price`, `description` |
| `orders` | 10 orders: `order_id`, `customer_id`, `product_id`, `order_date` |

Each order is for one product, bought by one customer. `orders.customer_id`
points to `customers` and `orders.product_id` points to `products`.

## Before you start

1. Make an account on [DoltHub](https://www.dolthub.com) and stay signed in.
2. Start a codespace on your copy of this repo and start your agent in the
   terminal.

If you already did Steps 1 to 4 of [make-your-own-database](../make-your-own-database/README-make-your-own-database.md) in this
codespace, Dolt is installed and you are logged in: skip to Step 3 below.

Copy each prompt below into the agent and press **Enter**. Wait for the agent
to finish and read what it did before you give it the next one. Replace the
parts in capitals with your own details.

## Step 1: Install Dolt

```default
Install Dolt and set it up with my name YOUR NAME and my DoltHub email YOUR EMAIL.
```

## Step 2: Log in to DoltHub

```default
Log me in to DoltHub.
```

The agent gives you a link. Open it, type a description such as `codespace`,
click **Create**, then tell the agent you are done. It checks that the login
worked.

## Step 3: Build the Database in the Codespace

```default
Create a new Dolt database in a folder called retail-orders/retail-orders (inside this exercise's folder). Load retail-orders/retail-orders.sql into it, show me the three tables and how many rows each has, then commit everything with the message "Create retail orders database".
```

The database now exists only in your codespace, in `retail-orders/retail-orders`.
Git ignores it (see `.gitignore`), so it never goes to GitHub: DoltHub is
where it gets shared.

## Step 4: Make an Empty Database on DoltHub

Do this one yourself, in the browser:

1. Go to <https://www.dolthub.com/profile> and click **Create Database**.
2. Name it `retail-orders`, make it **Public**, and click **Create**.

Leave it empty. Your push fills it.

## Step 5: Push to DoltHub

```default
Add my DoltHub database YOUR-DOLTHUB-USERNAME/retail-orders as the remote called origin and push main to it.
```

Refresh your database page on DoltHub. You should see the three tables and
your commit.

## Step 6: Change, Commit, Push

```default
Add me as a customer in the customers table and add an order for me for the Linen Dress. Show me what changed, commit it with a clear message, and push it to DoltHub.
```

On DoltHub, open **Commit Log** and click your newest commit to see exactly
which rows it added.

## What to Hand In

The link to your database on DoltHub, with at least two commits: the one that
created the database and the one that added you.
