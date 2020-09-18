Git
===

Install
-------

.. code-block:: bash

    $ sudo apt-get update
    $ sudo apt-get install git

After git is installed, set your account's default identity.

.. code-block:: bash

    $ git config --global user.email "you@example.com"
    $ git config --global user.name "Your name"

Setting SSH connection
----------------------

Before you generate an SSH key, check for any existing SSH keys.

.. code-block:: bash

    $ ls -al ~/.ssh
    # Lists the files in your .ssh directory, if they exist

If you don't have an existing public and private key pair, then generate a new SSH key.

.. code-block:: bash

    $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

This creates a new ssh key, using the provided email as a label.
When you're prompted to "Enter a file in which to save the key," press Enter.
This accepts the default file location.

To add the new key to ssh-agent, start the ssh-agent in the background.

.. code-block:: bash

    $ eval "$(ssh-agent -s)"
    > Agent pid 59566

Add your SSH private key to the ssh-agent.

.. code-block:: bash

    $ ssh-add ~/.ssh/id_rsa

Follow this `guide <https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account>`__
to add a new SSH key to your GitHub account.
