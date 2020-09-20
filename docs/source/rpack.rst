Building R package from scratch
===============================

The following is a short guide on how to create R package from scratch.

Setup
-----

First, we need to install ``devtools`` and ``roxygen2`` packages used to
automate the building process.

.. code-block:: bash

    $ conda install -c conda-forge r-devtools r-roxygen2

When it's done, we can create a framework for our R package, let's call it ``rpack``.

.. code-block:: bash

    $ R
    > devtools::create("rpack")

This will create a new directory called "rpack" with files ``DESCRIPTION``, ``NAMESPACE``
and empty subdirectory ``R``.

.. code-block:: bash

    $ cd rpack
    $ ls
    DESCRIPTION  NAMESPACE  R

Reference
---------

[1] H.Wickham, J.Bryan, `"R Packages" <https://r-pkgs.org/index.html>`__

[2] `"Making Your First R Package" <https://tinyheero.github.io/jekyll/update/2015/07/26/making-your-first-R-package.html>`__
