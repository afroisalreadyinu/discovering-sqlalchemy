Introduction
============

Python has a number of excellent tools to interface to relational
database systems, but SQLAlchemy shines among them. It is one of the
oldest, covers all popular database systems, is still under active
development, with new features coming up with every release, and the
code is of very high quality. Due to these reasons, it is the weapon
of choice of many organizations that want a feature-complete database
tool that is easy to use and integrate, is feature-rich, and can be
extended as needed when the necessity comes up.

The aim of this manual is to get you going with SQLAlchemy as rapidly
as possible, understand the basic machinery underlying it, and go
beyond the simple ORM queries to wield the full power of the RDBMS you
connect to. What can easily be found in the documentation (arguments
to methods, lists of classes etc.) will not be duplicated
here. Instead, the focus will be on patterns of SQLAlchemy use, and
how to create complex situations in a database, so that SQLAlchemy
code can be copied and tested rapidly. In order to do this, all
examples will include complete code to set up the database, and the
Python environment. The database setup code, and the SQLAlchemy
examples will target two RDBMSs supported by SQLAlchemy: PostgreSQL
and SQLite. PostgreSQL has become the weapon of choice for Python web
development due to its reliability and feature-completeness. SQLite is
a single-connection file-based RDBMS that has a great number of
features despite its small footprint, and comes built-in with
Python. Due to this reason, it's a great way to get going without
installing any separate software.

Installing a database system
----------------------------

To play around with a database, the first thing you need is a database
server, or just a file in the case of SQLite. If you want to use
SQLite, you can skip this section.

Thanks to modern package managers, installing PostgreSQL on MacOSX or
Linux should not be painful. On the Mac, the easiest way to get
PostgreSQL is to download the package installer from [the official
website](http://www.postgresql.org/download/macosx/), and run it. An
alternative way is to use a package manager such as
[Homebrew](http://brew.sh/). Afterwards, it's as easy as running `brew
install postgresql`.

### Configuring Postgres

Permissions are in `/usr/local/var/postgres/pg_hba.conf` on Mac
OSX. Logs are in `/usr/local/var/postgres/server.log`.

### Creating a database

Run `createdb -E UNICODE -O postgres sqlalchemydb` on the
commandline. To drop it, run `dropdb sqlalchemydb`.

Installing Python and Virtualenv
--------------------------------

Pretty much all Linux distros, and Mac OSX all come with Python
already installed. Just to make sure, you can open a terminal and type
`type python`, which should return `python is /usr/bin/python`. You
will definitely need virtualenv, though, to install SQLAlchemy and any
further packages without messing with your system Python distribution,
especially if you're on Linux. Refer to [the
website](http://virtualenv.readthedocs.org/en/latest/virtualenv.html#installation).

After you have installed virtualenv, run the following in the terminal
to create a virtual environment that will isolate your Python playground:

    mkdir -p ~/.virtualenvs
    virtualenv ~/.virtualenvs/sqlalchemy-env
    source ~/.virtualenvs/sqlalchemy-env/bin/activate

The commandline should now be prefixed with `(sqlalchemy-env)`. You
are now ready to install SQLAlchemy with the following command:

    pip install sqlalchemy

This will install the latest version of SQLAlchemy, 0.9.6 as of the
time of this writing. If you want to use PostgreSQL, you also have to
install psycopg2 with the following command:

    pip install psycopg2

### Testing whether you're ready to go

Start python in a terminal in which the virtualenv you installed
SQAlchemy in, and run the following:

    >>> from sqlalchemy import create_engine
    >>> engine = create_engine('postgresql://goodscloud:goodscloud@localhost:5432/sqlalchemydb')
    >>> engine.connect()

If you don't get a error such as `FATAL: database "sqlalchemydb" does
not exist`, you can carry on. From here on, any Python code involving
SQLAlchemy has to be run inside such a virtualenv.
