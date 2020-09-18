MongoDB
=======

Use this tutorial to install MongoDB Community Edition on Ubuntu 20.04 LTS using
the apt package manager.

Install MongoDB Community Edition
---------------------------------

Import the public key used by the package management system.

.. code-block:: bash

    $ wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -

The operation should respond with an ``OK``. However, if you receive an error indicating
that ``gnupg`` is not installed, install it and then retry importing the key.

.. code-block:: bash

    $ sudo apt-get install gnupg

Create a list file for MongoDB.

.. code-block:: bash

    $ echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list

Install the MongoDB packages.

.. code-block:: bash

    $ sudo apt-get update
    $ sudo apt-get install -y mongodb-org

Now start the ``mongod`` process by issuing the following command:

.. code-block:: bash

    $ sudo systemctl start mongod

If you receive an error similar to the following when starting mongod:

    **Failed to start mongod.service: Unit mongod.service not found.**

Then run the following command first:

.. code-block:: bash

    $ sudo systemctl daemon-reload

And then start the process again.

Verify that MongoDB has started successfully:

.. code-block:: bash

    $ sudo systemctl status mongod

You can optionally ensure that MongoDB will start following a system reboot
by issuing the following command:

.. code-block:: bash

    $ sudo systemctl enable mongod

As needed, you can stop the mongod process by issuing the following command:

.. code-block:: bash

    $ sudo systemctl stop mongod

You can restart the mongod process by issuing the following command:

.. code-block:: bash

    $ sudo systemctl restart mongod

Uninstall MongoDB Community Edition
-----------------------------------

To completely remove MongoDB from a system, you must remove the MongoDB
applications themselves, the configuration files, and any directories
containing data and logs.

Stop the mongod process by issuing the following command:

.. code-block:: bash

    $ sudo service mongod stop

Remove any MongoDB packages that you had previously installed.

.. code-block:: bash

    $ sudo apt-get purge mongodb-org*

Remove MongoDB databases and log files.

.. code-block:: bash

    $ sudo rm -r /var/log/mongodb
    $ sudo rm -r /var/lib/mongodb

MongoDB Compass
---------------

MongoDB Compass is the GUI for MongoDB. Can be downloaded from `official page <https://www.mongodb.com/try/download/compass>`__
and installed as following:

.. code-block:: bash

    $ sudo dpkg -i mongodb-compass_1.22.1_amd64.deb
