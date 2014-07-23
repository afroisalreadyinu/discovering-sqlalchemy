In this chapter, we will cover the basics of connecting to a database,
running statements, and interacting with a session. Let's add a very
simple table to our `sqlalchemydb` database. Connect to the database
with `psql sqlalchemydb`, and run the following SQL statement:

    CREATE TABLE users (
        id serial PRIMARY KEY,
	name varchar NOT NULL,
	email varchar NOT NULL );

And then connect to the same database with SQLAlchemy, and run a
query:

    from sqlalchemy import engine
    engine = create_engine('postgresql://postgres@localhost:5432/sqlalchemydb')
    conn = engine.connect()


Connection pool

Session