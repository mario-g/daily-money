# daily-money-mg
a daily expense tracking android app, forked by Mario Galizzi

I forked this application because I use it every day and I need some functional tweaks.
Dailymoney is the only Android application I found that implements double entry bookkeeping without crashing and giving you the possibility to export data to other systems using CSV. For example, GnuCash mobile kept crashing, and I don't really want to lose data.

https://en.wikipedia.org/wiki/Double-entry_bookkeeping_system

What I want to implement:
- *F1*: possibility to insert the real value of an account and check that the sum of the transactions equals the variation of the account
- *F2*: split transactions (every transactions can involve more than 2 accounts)

F1 goal:
- to check that all transactions are inserted into the system (it's important for cash, less important for bank account or cards), so that expense and income, which are used for budgeting purposes, represent reality
- for example, I could forget to track an expense or an income of money and budget for more or for less money because expense and income accounts are not consistent with what I have in my wallet and bank accounts

F1 details:
- given account A and dates d1 and d2, we know the real value of the account at the two dates. Let's call those values v1 and v2
- the "real value" v of an account A at date d is a function v(A, d). For example, v("wallet", "2016-12-25") gives the amount of cash in the wallet at Christmas 2016
- v(A, d) is not defined for every date d and every account A
- for every account A, we have a list of transactions involving it. We have a function t(A, startdate, enddate) which gives the variation of account A between the two dates
- a transaction "involves" an account A if it causes the balance of A to change
- function F1 checks that t(A, startdate, enddate) = v(A, enddate) - v(A, startdate) for every startdate and enddate available, and raises a warning that some income or expense is missing
