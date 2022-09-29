# CSI 3130 - Lab 2

Class: CSI 3130
Created: September 22, 2022 10:40 AM
Type: Lab

# Lab 2 - Exploring and working with postgresql

## Switch to the user created for postgresql in the previous lab

```bash
#To switch to the user
su  postgres
```

## Start the database server

```bash
postmaster –D $HOME/pgdb
```

## Open a new terminal window

```bash
#Switch to the postgres user
su  postgres
```

## Create a database

```bash
createdb test

#To open the terminal-based front-end to PostgreSQL "test" database type:
psql test
```

## Follow the instructions in the lab material attached to create tables, add/delete/modify values and more

[https://github.com/AnOnYmOuS219/CSI_3130_Fall_22/tree/main/labs/lab2](https://github.com/AnOnYmOuS219/CSI_3130_Fall_22/tree/main/labs/lab2)

You can find more commands here : [https://www.postgresql.org/docs/8.1/tutorial.html](https://www.postgresql.org/docs/8.1/tutorial.html)