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

Install R package from private repository
-----------------------------------------

If you want to install an R package from a private repository, first, you need
to set an SSH authentication in your account by adding your SSH keys. Then do the following.

.. code-block:: R

    creds <- git2r::cred_ssh_key(
        public = "~/.ssh/id_rsa.pub",
        private = "~/.ssh/id_rsa",
        passphrase = passphrase)

    devtools::install_git(
        url = "ssh_url_of_the_package",
        credentials = creds)

You can specify a specific branch of the repository as well. In that case,
just add branch="branch_name" to ``install_git`` options. Otherwise, it will always
default to the master branch.

Reference
---------

[1] H.Wickham, J.Bryan, `"R Packages" <https://r-pkgs.org/index.html>`__

[2] `"Making Your First R Package" <https://tinyheero.github.io/jekyll/update/2015/07/26/making-your-first-R-package.html>`__
