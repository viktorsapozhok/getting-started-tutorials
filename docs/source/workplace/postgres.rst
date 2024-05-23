PostgreSQL
==========

Here is how to install ``psql``, a terminal-based client for PostgreSQL database.

Install Postgres Client
-----------------------

If you need postgres client only, e.g. for login to database using ``psql``, then you can install it as follows.

.. code-block:: bash

    $ sudo apt-get install postgresql-client

Note, that client is included in PostgreSQL apt repository. So if you need it with database, then install it
as described in the next section.

Install PostgreSQL
------------------

Follow the `official guide <https://www.postgresql.org/download/linux/ubuntu/>`__ in case of questions.

Ubuntu includes PostgreSQL by default. To install PostgreSQL on Ubuntu, use the apt command:

.. code-block:: bash

    $ sudo apt install postgresql

Also install package ``libpq-dev`` and ``gcc`` (if not installed) to be able to
compile Python packages that depend on PostgreSQL, like ``psycopg2-binary``.

.. code-block:: bash

    $ sudo apt install libpq-dev gcc

Uninstall PostgreSQL
--------------------

The simplest way to do this is to open a terminal and type:

.. code-block:: bash

    $ sudo apt-get --purge remove postgresql

This will also prompt you to remove that software that depends on Postgres.
It is possible that Postgres installs itself in several parts. In that case, a simple:

.. code-block:: bash

    $ dpkg -l | grep postgres

Will get you the list of those packages that Postgres installed. Then, just use
the same "apt-get --purge remove ...." command but instead of just postgresql,
type each package name, separated by spaces, like:

.. code-block:: bash

    $ sudo apt-get --purge remove postgresql-client-13 postgresql-client-common pgdg-keyring

As a next step, remove the following folders:

.. code-block:: bash

    $ sudo rm -rf /var/lib/postgresql/
    $ sudo rm -rf /var/log/postgresql/
    $ sudo rm -rf /etc/postgresql/

And finally, remove the postgres user and group:

.. code-block:: bash

    $ userdel -r postgres
    $ groupdel postgres

That's it.
