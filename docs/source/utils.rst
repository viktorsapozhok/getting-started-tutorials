Utilities
=========

Midnight Commander
------------------

GNU Midnight Commander is a free cross-platform orthodox file manager.
To install it, you need to enable the universe repository, then update and install.

.. code-block:: bash

    $ sudo add-apt-repository universe
    $ sudo apt update
    $ sudo apt install mc

Shutter
-------

Shutter is a tool for taking screenshots in Linux. You can take and edit screenshots with it.

.. code-block:: bash

    $ sudo add-apt-repository -y ppa:linuxuprising/shutter
    $ sudo apt install shutter

To uninstall shutter, you need first to remove it from your system.

.. code-block:: bash

    $ sudo apt remove shutter

Next, remove the PPA from your list of repositories.

.. code-block:: bash

    $ sudo add-apt-repository --remove ppa:linuxuprising/shutter

Google Chrome
-------------

Download .deb package from the `official page <https://www.google.com/chrome/>`__
and install it as follows:

.. code-block:: bash

    $ cd Downloads
    $ sudo dpkg -i google-chrome-stable_current_amd64.deb

DBeaver
-------

DBeaver is free and open source universal database UI. It can be easily installed
via snap:

.. code-block:: bash

    $ sudo snap install dbeaver-ce

MongoDB Compass
---------------

MongoDB Compass is the GUI for MongoDB. Can be downloaded from `official page <https://www.mongodb.com/try/download/compass>`__
and installed as following:

.. code-block:: bash

    $ sudo dpkg -i mongodb-compass_1.22.1_amd64.deb


