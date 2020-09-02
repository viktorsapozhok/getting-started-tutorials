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
