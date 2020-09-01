Miniconda
=========

Miniconda is a free minimal installer for conda. It includes only conda, Python,
the packages they depend on, and a small number of other useful packages,
including pip, zlib and a few others.

Download the installer from `here <https://docs.conda.io/en/latest/miniconda.html#linux-installers>`__
and run it.

.. code-block:: bash

    $ sh Miniconda3-latest-Linux-x86_64.sh

When it's installed, open ``~/.bashrc`` and copy lines in the end starting with
``# >>> conda initialize >>>`` and paste it to ``~/.zshrc`` in the end of file.