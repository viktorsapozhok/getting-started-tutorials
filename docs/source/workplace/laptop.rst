Dell Inspiron Laptop
====================

Disable touchscreen
-------------------

To disable the touchscreen input permanently, find your touchscreen XID and disable it.

.. code-block:: bash

    $ xinput --list
    # Lists your devices

    $ xinput disable [XID]

Open your startup applications.

.. code-block:: bash

    $ gnome-session-properties

Click Add and enter the ``disable`` command to be executed at login (name and comment are optional).

Change close lid action
-----------------------

Open the ``/etc/systemd/logind.conf`` file in a text editor as root.

.. code-block:: bash

    $ sudo gedit /etc/systemd/logind.conf

Change the line

.. code-block:: bash

    #HandleLidSwitch=ignore

To this line:

.. code-block:: bash

    HandleLidSwitch=hibernate

And restart service.

.. code-block:: bash

    $ sudo service systemd-logind restart
