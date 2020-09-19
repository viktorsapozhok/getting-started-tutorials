Getting started with mongo shell
================================

The mongo shell is an interactive JavaScript interface to MongoDB.
You can use the mongo shell to query and update data as well as perform
administrative operations.

The mongo shell is included as part of the MongoDB server installation.
If you have already installed the server, the mongo shell is installed
to the same location as the server binary.

Connect to DB
-------------

You can run mongo shell without any command-line options to connect to a
MongoDB instance running on your localhost with default port 27017.

.. code-block:: bash

    $ mongo
    MongoDB shell version v4.4.1
    connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
    Implicit session: session { "id" : UUID("81ccbc3b-be5a-4782-ab69-371df1e447f9") }
    MongoDB server version: 4.4.1
    ...

You can view help information using ``help`` command from the shell.

.. code-block:: bash

    > help
            db.help()                    help on db methods
            db.mycoll.help()             help on collection methods
            ...

To list all the databases available to the user, use the helper ``show dbs``.
To check the database you are currently connected, use ``db`` command.
By default, the ``test`` database is used.

.. code-block:: bash

    > show dbs
    admin   0.000GB
    config  0.000GB
    local   0.000GB
    > db
    test

.. note::

    The "test" database is not shown in the list of databases as it's empty.
    When you create the first collection, it will appear in the list.

You can switch to non-existing databases. When you first store data in
the database, such as by creating a collection, MongoDB creates the database.
For example, the following creates both the database "newdb" and
the collection "newcol" during the insertOne() operation.

.. code-block:: bash

    > use newdb
    switched to db newdb

    > db.newcol.insertOne({x: 1});
    {
        "acknowledged" : true,
        "insertedId" : ObjectId("5f65e61e68c2bd77c77735a0")
    }

    > show dbs
    admin   0.000GB
    config  0.000GB
    local   0.000GB
    newdb   0.009GB

Let's create a new user for "newdb" database.

.. code-block:: bash

    > db
    newdb

    > db.createUser({
    ...     user: "user",
    ...     pwd: "password",
    ...     roles: [{
    ...         role: "readWrite",
    ...         db: "test"
    ...     }]
    ... });
    Successfully added user
    ...
    > exit

To connect to "newdb" as user, you need to specify the username and password.

.. code-block:: bash

    $ mongo -u user -p password newdb
    > db
    newdb

Import geojson with mongoimport
-------------------------------

The mongoimport tool imports content from an CSV, TSV or JSON data into MongoDB.
Let's use it to bulk import countries.geojson to "countries" collection in "newdb"
database.

.. code-block:: bash

    $ cat countries.geojson
    [{"type": "Feature", "id": 0, "properties": {"name": "Afghanistan"}, "geometry": {"type": "Point", "coordinates": [67.70995, 33.93911]}},
    {"type": "Feature", "id": 1, "properties": {"name": "Albania"}, "geometry": {"type": "Point", "coordinates": [20.1683, 41.1533]}},
    {"type": "Feature", "id": 2, "properties": {"name": "Algeria"}, "geometry": {"type": "Point", "coordinates": [1.6596, 28.0339]}},
    ...
    {"type": "Feature", "id": 185, "properties": {"name": "US"}, "geometry": {"type": "Point", "coordinates": [-100.0, 40.0]}}]

    $ mongoimport --db newdb -u user -p password -c countries --file countries.geojson --jsonArray
    2020-09-19T14:31:31.451+0200	connected to: mongodb://localhost/
    2020-09-19T14:31:31.457+0200	186 document(s) imported successfully. 0 document(s) failed to import.

Now we connect to the database and list all the collections.

    $ mongo -u user -p password newdb
    > db.getCollectionNames()
    [ "countries", "newcol" ]

