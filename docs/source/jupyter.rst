Jupyter notebook to PDF in a few lines
======================================

While working on our Jupyter notebook, sometimes we want to share our processed dataset
complete with the created plot and the markdown explanation we already created in a readable form.
There is an easy way to turn our Jupyter notebooks into PDF files. Just with a simple setup,
you can access your notebook as a PDF.

First, you need to install the Python package called "notebook-as-pdf":

.. code-block:: bash

    $ pip install notebook-as-pdf
    $ pyppeteer-install

The second command will download and setup Chromium. It is used to perform the HTML to PDF conversion.

.. note::

    On linux you probably also need to install some or all of the APT packages listed in `binder/apt.txt <https://github.com/betatim/notebook-as-pdf/blob/master/binder/apt.txt>`__.

Now to convert notebook to PDF, simply use this command:

.. code-block:: bash

    $ jupyter-nbconvert --to PDFviaHTML example.ipynb --no-input

This will create a file called example.pdf.

Reference
---------

[1] `github.com/betatim/notebook-as-pdf <https://github.com/betatim/notebook-as-pdf>`__


