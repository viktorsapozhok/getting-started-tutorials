R
=

R Base
------

To install R on Ubuntu 20.04, update the package index and install it.

.. code-block:: bash

    $ sudo apt update
    $ sudo apt install r-base

Confirm the R installation by checking its version:

.. code-block:: bash

    $ R --version

Access R shell:

.. code-block:: bash

    $ R

To install the actual R library package enter:

.. code-block:: bash

    $ sudo apt install r-cran-ggplot2

Test the library installation by loading it from R shell

.. code-block:: bash

    $ R
    > library(ggplot2)

RStudio
-------

First, you need to install all the prerequisites. Open up a terminal and enter:

.. code-block:: bash

    $ sudo apt update
    $ sudo apt -y install gdebi-core

Download the RStudio .deb package from `official website <https://rstudio.com/products/rstudio/download/#download>`__
and install it as follows:

.. code-block:: bash

    $ cd Downloads
    $ sudo gdebi rstudio-1.3.1073-amd64.deb

Conda + R
---------

To install R in the existing environment, use this command:

.. code-block:: bash

    $ conda install -c r r-base

To create a new environment with R, use this:

.. code-block:: bash

    $ conda create -n r_env r-base
    $ conda activate r_env
    $ R --version

To launch RStudio from conda environment, you need first to activate it in a shell
session and then launch.

.. code-block:: bash

    $ conda activate r_env
    $ rstudio &

Ending the command with ``&`` enables one to continue using shell, or close it, without
affecting RStudio instance.

Once in RStudio, you can verify that values of ``R.home()`` and ``.libPaths()`` point
to the environment-specific location.

Use this command to install R packages via conda:

.. code-block:: bash

    $ conda install -c r r-packageName

Reference
---------

[1] How to setup conda installed R with RStudio
(`link <https://stackoverflow.com/questions/38534383/how-to-set-up-conda-installed-r-for-use-with-rstudio>`__)

[2] List of R packages available in Anaconda
(`link <http://repo.anaconda.com/pkgs/r/>`__)