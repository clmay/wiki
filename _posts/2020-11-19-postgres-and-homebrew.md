---
layout: post
title: Postgres and Homebrew
intro: A few pesky, undocumented steps for setup
---

I'm writing this as much for my future self, as I am for anyone else. But who
knows? Maybe you find yourself in the same position in which I found myself for
most of the day: having spent more time than you'd like to admit, trying to
figure out why a database migration you were trying to run kept failing...

If so, allow me to try to save you a little time.

After installing Postgres via `brew install postgresql`, you're likely to
encounter one of several errors when you try to perform database-related tasks:

- `FATAL: database "postgres" does not exist`
- `FATAL: role "postgres" does not exist`

You see, when installing Postgres, Homebrew, in its infinite wisdom, does _not_
create the _default database_ that Postgres expects _by default_. Even though it
seems like it probably should... 😉

### Creating your user's database

You can easily remedy this. At a terminal, run `psql`. You should see an error
like `FATAL: database "<missing-database-name>" does not exist`. Usually, the
value replacing `<missing-database-name>` is your username.The first thing to
do, is create that database:

```sh
createdb <missing-database-name> # again, this should probably be your username, a.k.a. whatever is printed when you run `whoami` in a terminal
```

Congrats on the new database, `<you-handsome-devil-you>`.

Now that your user has its database, you'll be able to drop into `psql`, and
it's time to setup the `postgres` database and user:

```sh
psql # this will enter you into the `psql` shell; notice the prompt has now changed to `postgres=#`?

# now it's time to run some PSQL commands...

# so, create the `postgres` user
CREATE USER postgres SUPERUSER;

# verify the new user was created succcessfully
# note: the name must show as exactly `postgres`, and must be listed as a `Superuser`
\du # (the command to list users; a handy one)

# and now create the `postgres` database
CREATE DATABASE postgres WITH OWNER postgres;

# verify the database was create succesfully
# note: the name must be exactly `postgres`, and must have an `Owner` of `postgres`
\l # (the command to list databases; also handy)
```

Try running your database tasks again. You should be set. Not too hard, was it?
But it can be difficult to figure out from scratch if you're not already a
strong `psql`-ite.

P.S. Perhaps there are really great reasons that Homebrew deviates from Postgres
defaults, and I'm just not privy to them. If so, and someone can either explain
or point me to documentation for those reasons, I am happy to update this post
accordingly. But until then, since these steps weren't in the Homebrew
documentation for the formula, _nor_ the Postgres website's page for
installation via Homebrew, I will continue to throw shade 🕶
