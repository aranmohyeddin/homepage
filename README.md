# homepage
My personal homepage

## Some stuff that I learnt during this but I might forget later:

### How I made this repo:
```
django-admin startproject homepage
cd homepage
git init
git add .
git commit -m 'initial commit'
git remote add origin git@github.com:aranmohyeddin/homepage.git
git pull origin master --allow-unrelated-histories
git push -u origin master
```

### Setting up postgresql:
[Archwiki guide for postgreSQL](https://wiki.archlinux.org/index.php/PostgreSQL)
I was told by someone with decades of experience to:
Create three users: 
 * One to own and control the schema.
 * Another that can to INSERT/UPDATE/DELETE.
 * A third that can only read.
Under no circumstances should one application be controlling the schema and yes, there are always multiple applications.
Sadly, ORMs are an example of a mistake that a lot of people make over long stretches of time 
I strongly recommend against it. go with a DAL instead
ORM == "pretend SQL doesn't exist"
DAL == "Write the SQL and hook it up yourself"
The reason to have three users is to limit the damage malice or mistakes can cause
You don't know what's gonna be on there into a long future. the process of creating and using separate users is cheap now. it will be VERY expensive if you attempt it later
If you insist on using an ORM, do *NOT* use the parts that let it touch the schema. Write that yourself.
So you form good habits :) and so you understand what you're doing :) :)
Codd was quite prescient on this score, right down to the title of his paper: A Relational Model of Large, *Shared* Data Banks

Another person said:
if you let your code drive your data, then the data will only ever be useful for that specific code.    if you design your data around your problem space, then write code for the applications, the data becomes useful for a range of applications that can access it.

I tried to get it done this way but I spent a lot of time and couldn't figure how I should implement it exactly so I will just do it the easy way for now which seems to be [This stackoverflow answer](https://stackoverflow.com/a/42050358/5120089):

From the django doc, I uncommented this in `/var/lib/postgres/data/postgresql.conf`

    default_transaction_isolation: 'read committed'

### Hiding secret key and db password from git:
Created two files in project containing those sensitive information, and did the appropriate things is settings.py
Added the path relative to .git into my .git/info/exclude.
verified with git status.

