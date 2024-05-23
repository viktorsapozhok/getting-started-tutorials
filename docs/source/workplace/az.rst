Azure CLI
=========

To install Azure check the latest available version `here <https://learn.microsoft.com/en-us/cli/azure/install-azure-cli>`__.

The Azure CLI team maintains a script to run all installation commands in one step.
This script is downloaded via curl and piped directly to bash to install the CLI.

.. code-block:: bash

    $ curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

Create environment aliases for your ``A`` and ``B`` account directories (if you have ones),
let's say ``AZ_CONFIG_DIR_A`` and ``AZ_CONFIG_DIR_B``.

.. code-block:: bash

    $ export AZ_CONFIG_DIR_A=/home/user/.config/azure/username_a
    $ export AZ_CONFIG_DIR_B=/home/user/.config/azure/username_b

Create local directories for accounts.

.. code-block:: bash

    $ mkdir -p $AZ_CONFIG_DIR_A
    $ mkdir -p $AZ_CONFIG_DIR_B

Login to Azure CLI.

.. code-block:: bash

    $ export AZURE_CONFIG_DIR=$AZ_CONFIG_DIR_A
    $ az login

Do the same for ``B`` account.

Install ``ssh`` extension to be able to login to servers using ssh.

.. code-block:: bash

    $ az extension add --name ssh

Download and install ``kubectl``, the Kubernetes command-line tool. Download and
install ``kubelogin``, a client-go credential plugin implementing azure authentication.

See `here <https://learn.microsoft.com/en-us/cli/azure/aks?view=azure-cli-latest#az-aks-install-cli>`__ for more information.

.. code-block:: bash

    $ az aks install-cli

By default, ``kubectl`` and ``kubelogin`` are installed in ``/usr/local/bin``.
Update your ``PATH`` environment variable to include the directory where ``kubectl``
and ``kubelogin`` are installed.

.. code-block:: bash

    $ export PATH="/usr/local/bin:$PATH"
