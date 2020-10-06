Create an Azure service principal with Azure CLI
================================================

An Azure service principal is an identity created to access Azure resources.
This access is restricted by the roles assigned to the service principal,
giving you control over which resources can be accessed and at which level.

.. note::

    For security reasons, it's always recommended to use service principals
    with automated tools rather than allowing them to log in with a user identity.

Install the Azure CLI
---------------------

The Azure command-line interface (Azure CLI) is a set of commands used
to create and manage Azure resources. It can be installed with following command:

.. code-block:: bash

    $ curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

Manage Azure subscription
-------------------------

After Azure CLI is installed, you can manage your account using ``az account``
directive. For example, to get the details of a subscription use following:

.. code-block:: bash

    $ az account show

To list the resource groups your account is subscribed on, use the subscription
ID returned in the output of the previous command.

.. code-block:: bash

    $ az group list --subscription SubID

Create a service principal
--------------------------

To get a list of service principals you are owned, issue the following:

.. code-block:: bash

    $ az ad sp list --show-mine

To create a new service principal with password-based authentication, provide the
space-separated list of scopes the service principal's role applies to. The scope
format is given by the string ``/subscriptions/{SubID}`` or ``/subscriptions/{SubID}/resourceGroups/{ResourceGroup}``.

For example, to create a service principal applied to all resources available
to group "Research", use following:

.. code-block:: bash

    $ az ad sp create-for-rbac --name RESEARCH_SERVICE_PRINCIPAL --scopes /subscriptions/{SubID}/resourceGroups/Research

The output for a service principal with password authentication includes
the password key. Make sure you copy this value - it can't be retrieved.

.. note::

    If you forget the password, reset the service principal credentials.

The ``appId`` and ``tenant`` keys appear in the output of ``az ad sp create-for-rbac``
and are used in service principal authentication. Record their values,
but they can be retrieved at any point with ``az ad sp list``.

The default role for a service principal is Contributor. This role has full permissions
to read and write to an Azure account. The Reader role is more restrictive,
with read-only access. For more information on Role-Based Access Control
and roles, see `RBAC: Built-in roles <https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-built-in-roles>`__.

Configure access policies on resources
--------------------------------------

Keep in mind, you might need to configure permissions on resources
that your principal needs to access. For example, you must update a key vault's access
policies to give your service principal access to keys, secrets, or certificates.

#. In the Azure portal, navigate to your key vault and select **Access policies**.
#. Select **Add access policy**, then select the key, secret, and certificate permissions you want to grant your application. Select the service principal you created previously.
#. Select **Add** to add the access policy, then **Save** to commit your changes.

.. image:: /_static/images/add_principal_access_policies.png
    :align: center
