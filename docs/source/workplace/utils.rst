Utilities
=========

Build-essential
---------------

The build-essentials packages are the form of meta-packages that are essential to
compile software. They contain the GNU/g++ compiler collection, GNU debugger,
and a few more libraries and tools that are needed for compiling a program.

.. code-block:: bash

    $ sudo apt-get install build-essential gcc libpq-dev

Midnight Commander
------------------

GNU Midnight Commander is a free cross-platform orthodox file manager.
To install it, you need to enable the universe repository, then update and install.

.. code-block:: bash

    $ sudo add-apt-repository universe
    $ sudo apt update
    $ sudo apt install mc

LibreOffice
-----------

If LibreOffice is not installed by default, you can install it by running the following command:

.. code-block:: bash

    $ sudo apt install libreoffice

yq (YAML Processor)
-------------------

``yq`` is a lightweight and portable command-line YAML processor.
It can be used to process and manipulate YAML files. It can be installed via snap.

.. code-block:: bash

    $ snap install yq

Check `github repo <https://github.com/mikefarah/yq>`__ for more information.

Google Chrome
-------------

Download .deb package from the `official page <https://www.google.com/chrome/>`__
and install it as follows:

.. code-block:: bash

    $ cd Downloads
    $ sudo dpkg -i google-chrome-stable_current_amd64.deb
