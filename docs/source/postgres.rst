Getting started with PostgreSQL
===============================

PostgreSQL, also known as Postgres, is a free and open-source relational database
management system, emphasizing extensibility and technical standards compliance.
It is designed to handle a range of workloads, from single machines to data warehouses
or web services with many concurrent users. This guide is to give a basic
understanding of “How to work with Postgres”.

Create user
-----------

Once the installation is complete, you should add and configure a role for your
Ubuntu user so that you can easily enter the PostgreSQL environment and begin commanding the db.

First, sign into the default ‘postgres’ user:

.. code-block:: bash

    $ sudo su - postgres
    postgres@alex:~$

Enter the PostgreSQL environment as follows:

.. code-block:: bash

    postgres@alex:~$ psql
    psql (13.0 (Ubuntu 13.0-1.pgdg20.04+1))
    Type "help" for help.

    postgres=#

Once you login you can view the Databases & Roles by giving the commands ``\list`` (list out the databases)
and ``\du`` (list out the roles).

.. code-block:: bash

    postgres=# \list
                                      List of databases
       Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
    -----------+----------+----------+-------------+-------------+-----------------------
     postgres  | postgres | UTF8     | en_GB.UTF-8 | en_GB.UTF-8 |
     template0 | postgres | UTF8     | en_GB.UTF-8 | en_GB.UTF-8 | =c/postgres          +
               |          |          |             |             | postgres=CTc/postgres
     template1 | postgres | UTF8     | en_GB.UTF-8 | en_GB.UTF-8 | =c/postgres          +
               |          |          |             |             | postgres=CTc/postgres
    (3 rows)

    postgres=# \du
                                       List of roles
     Role name |                         Attributes                         | Member of
    -----------+------------------------------------------------------------+-----------
     postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

    postgres=# \q

You can create a new role by using the below command from your terminal:

.. code-block:: bash

    postgres@alex:~$ createuser --interactive
    Enter name of role to add: alex
    Shall the new role be a superuser? (y/n) y
    postgres@alex:~$ psql
    psql (13.0 (Ubuntu 13.0-1.pgdg20.04+1))
    Type "help" for help.

    postgres=# \du
                                       List of roles
     Role name |                         Attributes                         | Member of
    -----------+------------------------------------------------------------+-----------
     alex      | Superuser, Create role, Create DB                          | {}
     postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

Use ``createuser --interactive --pwprompt`` to create a new role with password authentication.

You can remove a role using ``DROP ROLE`` statement:

.. code-block:: bash

    postgres=# DROP ROLE alex;

Create a database
-----------------

Make sure you’re switched as a postgres user, if not use the below command ``sudo -i -u postgres``.

.. code-block:: bash

    postgres@alex:~$ createdb research

When it's created, you can connect to it from shell:

.. code-block:: bash

    $ psql -U alex -d research
    research=#

To grant the connect access to the database, use following:

.. code-block:: bash

    postgres=# GRANT CONNECT ON DATABASE dbname TO username;

Create an Azure Database
------------------------

Follow `this guide <https://docs.microsoft.com/en-us/azure/postgresql/quickstart-create-server-database-portal>`__
to create an Azure Database for PostgreSQL server by using the Azure portal. When its created and the firewall rule
configured, you can connect to the server via psql client.

.. note::

    Use the empty database ``postgres`` with admin user.

Run the following command in shell terminal replacing values with your actual server name and admin user login name:

.. code-block:: bash

    psql --host=mydemoserver.postgres.database.azure.com --port=5432 --username=myadmin@mydemoserver --dbname=postgres

List the available databases by issuing ``\list`` command:

.. code-block:: bash

    psql (13.1 (Ubuntu 13.1-1.pgdg20.04+1), server 11.6)
    SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
    Type "help" for help.

    postgres=> \list
                                                                   List of databases
           Name        |      Owner      | Encoding |          Collate           |           Ctype            |          Access privileges
    -------------------+-----------------+----------+----------------------------+----------------------------+-------------------------------------
     azure_maintenance | azure_superuser | UTF8     | English_United States.1252 | English_United States.1252 | azure_superuser=CTc/azure_superuser
     azure_sys         | azure_superuser | UTF8     | English_United States.1252 | English_United States.1252 |
     postgres          | azure_superuser | UTF8     | English_United States.1252 | English_United States.1252 |
     template0         | azure_superuser | UTF8     | English_United States.1252 | English_United States.1252 | =c/azure_superuser                 +
                       |                 |          |                            |                            | azure_superuser=CTc/azure_superuser
     template1         | azure_superuser | UTF8     | English_United States.1252 | English_United States.1252 | =c/azure_superuser                 +
                       |                 |          |                            |                            | azure_superuser=CTc/azure_superuser
    (5 rows)

Now you can create a new database.

.. code-block:: bash

    postgres=> CREATE DATABASE research;
    CREATE DATABASE

Mission completed!

Create schema
-------------

To create a new schema, execute the following from the postgres shell:

.. code-block:: bash

    postgres=# CREATE SCHEMA new_schema;

To give access to a user, use following:

.. code-block:: bash

    postgres=# GRANT USAGE ON SCHEMA schema_name TO username;
    postgres=# GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA schema_name TO username;

Copy table from one database to another
---------------------------------------

To copy a table from one database to another we first need to extract table into a
script file and then upload it from script to the target database. We use ``pg_dump``
utility for dumping table into a script.

.. code-block:: bash

    pg_dump --host=HOST --port=PORT --username=USER --dbname=DB --format=plain --verbose --file=TABLE.sql --table TABLE --data-only

Next, we delete data from the table in target database:

.. code-block:: bash

    db=> DELETE FROM table WHERE 1=1;

Upload table data from the script file.

.. code-block:: bash

    psql --host=HOST --port=PORT --username=USER --dbname=TARGET_DB --file=TABLE.sql

Reset primary key sequence when it falls out of sync
----------------------------------------------------

Login to database and run the following:

.. code-block:: bash

    SELECT MAX(id) FROM your_table;

The run the following. The result should be higher than the last one.

.. code-block:: bash

    SELECT nextval('your_table_id_seq');

If it's not higher then lock the table to protect against the concurrent inserts
and update the counter.

.. code-block:: bash

    BEGIN;
        LOCK TABLE your_table IN EXCLUSIVE MODE;
        SELECT setval('your_table_id_seq', COALESCE((SELECT MAX(id)+1 FROM your_table), 1), false);
    COMMIT;

Remove role
-----------

To remove a user with all his privileges, issue the following from postgres terminal:

.. code-block:: bash

    db=> DROP OWNED BY user;
    db=> DROP USER user;

DBeaver
-------

DBeaver is free and open source universal database UI. To install it, download ``.deb`` package from `here <https://dbeaver.io/download/>`__
and install it using ``dpkg``.

.. code-block:: bash

    $ sudo dpkg -i dbeaver-ce_22.3.5_amd64.deb
