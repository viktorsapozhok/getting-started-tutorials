Using R with conda
==================

R programming language and over 6.000 commonly used R packages can be easily
installed with Anaconda.

Creating an environment with R
------------------------------

When creating a new environment, you can use R by explicitly including r-base
in list of packages.

.. code-block:: bash

    $ conda create --name new_env r-base
    $ conda activate new_env

If channel is not specified then r channel is used by default. Always verify
a version of installed R package as the latest package release is not
necessary provided by default channel.

You can find the current version of a specific package using ``conda search``.

.. code-block:: bash

    $ conda search -c conda-forge r-base
    # Name                       Version           Build  Channel
    r-base                         3.6.1      hce969dd_0  pkgs/r
    r-base                         4.0.2      he766273_1  conda-forge

.. note::

    Use ``conda-forge`` channel to install the latest R version.

You can specify the channel when creating the environment.

.. code-block:: bash

    $ conda create --name new_env -c conda-forge r-base

Installing R packages
---------------------

When using conda to install R packages, you will need to add r- before
the regular package name. For instance, if you want to install rbokeh,
you will need to use conda install r-rbokeh or for rJava, type conda install r-rjava.

.. code-block:: bash

    $ conda install -c r r-packageName
    $ conda install -c conda-forge r-packageName

To list the packages in the environment use this:

.. code-block:: bash

    $ conda list

To remove package from the environment:

.. code-block:: bash

    $ conda remove r-packageName

RStudio from environment
------------------------

To launch RStudio from conda environment, you need first to activate it in a shell
session and then launch.

.. code-block:: bash

    $ conda activate new_env
    $ rstudio &

Ending the command with ``&`` enables one to continue using shell, or close it, without
affecting RStudio instance.

Once in RStudio, you can verify that values of ``R.home()`` and ``.libPaths()`` point
to the environment-specific location.

.. note::

    With the R plugin installed in PyCharm, you can get native support for ``.R`` files.
    The advantage of using PyCharm is that, in contrast with RStudio, it supports conda
    virtual environments.
