# Make Your Own Database with the Agent

**Start here.** This exercise also sets up Dolt in your codespace and logs
you in to DoltHub. The other exercises use that same setup.

**Your job:** create a database with **2 tables and 1 foreign key** that
connects them, on a topic you choose. The agent dreams up the tables and
made-up data with you. First it installs Dolt and logs you in to DoltHub.
Then it helps you build the database and share it on DoltHub.

A **foreign key** is a column in one table that must match the key of a row
in the other table. It's what connects the two tables: for example, if one
table lists a coffee shop's drinks and the other its orders, each order's
`drink_id` must be a drink that's really on the menu.

## Before you start

1. **Make a DoltHub account.** Go to <https://www.dolthub.com>, click
   **Sign Up**, and follow the steps (you'll get an email to confirm your
   account). Write down your DoltHub **username** and the **email** you used.
2. **Stay signed in to DoltHub** in a browser tab. You'll need it in Step 3.
3. **Start a codespace** on your copy of this repo and start your agent in the
   terminal.

Copy each prompt into the agent and press **Enter**. Read what the agent says
before you go on. Replace the parts in capitals with your own details. If the
agent asks to install something or run a command, allow it.

## Step 1: Install Dolt

```default
Install Dolt in this codespace and show me that it works.
```

The agent installs Dolt and shows its version number, for example
`dolt version 2.7.3`.

## Step 2: Tell Dolt Who You Are

Dolt puts your name and email on every change you save (every **commit**), so
people can see who made it. Use the email of your DoltHub account.

```default
Set up Dolt with my name YOUR NAME and my DoltHub email YOUR EMAIL, and show me the settings.
```

## Step 3: Log In to DoltHub

To put your database on DoltHub, Dolt in your codespace needs permission to
use your DoltHub account. It gets that with a **key**: a long code that the
agent makes and you add to your account.

```default
Log me in to DoltHub. My DoltHub username is YOUR-DOLTHUB-USERNAME.
```

1. The agent gives you a link that starts with
   `https://www.dolthub.com/settings/credentials`. Click it (or copy it into
   your browser). Make sure you are signed in to DoltHub.
2. DoltHub opens the **Credentials** page with the key already filled in. If
   the key box is empty, copy the key from the agent's message and paste it
   in.
3. In **Description**, type `codespace`. Click **Create**.
4. Go back to the agent and type `done`.

## Step 4: Check You Are Logged In

```default
Check that I'm logged in to DoltHub, and tell me which username Dolt is using.
```

The agent should say you are logged in as **your** DoltHub username. If it
says the key isn't working, go back to Step 3: the key probably wasn't added
on the Credentials page.

You only need to do Steps 1 to 4 once in each codespace. If you delete the
codespace and make a new one, do them again.

## Step 5: Dream Up the Database

Pick your topic. Then:

```default
Dream up a small practice database about YOUR TOPIC. Give it two tables connected by one foreign key, with 5 to 10 rows of made-up data in each. Don't create anything yet: explain in plain words what each table holds, its columns, its primary key, and how the foreign key connects the tables. Show me a few example rows.
```

Check the design before you go on. It must have **exactly 2 tables and 1
foreign key**. If it has more tables or keys, or no foreign key, ask the agent
to fix it. If you want other changes (another column, different data, more
rows), tell the agent. Make sure you can answer:

- What is the primary key of each table?
- Which column is the foreign key, and which table does it point to?

## Step 6: Build It

Choose a short name for your database, with dashes instead of spaces, such
as `coffee-shop` or `sneaker-collection`.

```default
Save the design as a SQL file called make-your-own-database/DATABASE-NAME.sql. Then create a new Dolt database in the folder make-your-own-database/DATABASE-NAME, load the SQL file into it, show me both tables, and commit it with a message that says what the database is.
```

## Step 7: Ask Questions

```default
Suggest three interesting questions about my data that need both tables. Answer each one with SQL that joins the tables, and show me the SQL.
```

## Step 8: Share It on DoltHub

On DoltHub, go to <https://www.dolthub.com/profile> and click
**Create Database**. Give it the same name as your database
(`DATABASE-NAME`), make it **Public**, and click **Create**. Leave it empty.

```default
Add my DoltHub database YOUR-DOLTHUB-USERNAME/DATABASE-NAME as the remote called origin and push main to it. Then give me the DoltHub links to my database and to each of its two tables.
```

Open the links. On DoltHub, open **Commit Log** to see your commit.

## What to Hand In

1. The link to your database on DoltHub. It must have 2 tables and 1
   foreign key.
2. Short answers, in your own words:
   - What are your two tables, and what is the primary key of each?
   - What is the foreign key, and which table does it point to?
   - Which of the three questions in Step 7 was most interesting, and what
     was the answer?
