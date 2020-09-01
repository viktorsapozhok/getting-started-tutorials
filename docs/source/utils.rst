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

