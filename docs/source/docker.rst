Docker
======

Install Docker Engine
---------------------

Update software repositories to make sure you've got access to the latest revisions.

.. code-block:: bash

    $ sudo apt-get update

Uninstall old versions of docker before proceeding using this command:

.. code-block:: bash

    $ sudo apt-get remove docker docker-engine docker.io

Install docker.

.. code-block:: bash

    $ sudo apt install docker.io

Setup docker service to be running at startup.

.. code-block:: bash

    $ sudo systemctl start docker
    $ sudo systemctl enable docker

Test the installation verifying docker version.

.. code-block:: bash

    $ docker --version

Install Docker Compose
----------------------

Compose is a tool for defining and running multi-container Docker applications.
With Compose, you use a YAML file to configure your application’s services.
Then, with a single command, you create and start all the services from your configuration.

Run this command to download the current stable release of Docker Compose:

.. code-block:: bash

    $ sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

.. note::

    To install a different version of Compose, substitute 1.26.2 with the version of Compose you want to use.

Apply executable permissions to the binary.

.. code-block:: bash

    $ sudo chmod +x /usr/local/bin/docker-compose

Test the installation.

.. code-block:: bash

    $ docker-compose --version
    docker-compose version 1.26.2, build 1110ad01

Run docker as non-root user
---------------------------

If you want to run docker as non-root user then you need to add it to docker group.
First, create the docker group if it doesn't exist.

.. code-block:: bash

    $ sudo groupadd docker

Add your user to the docker group.

.. code-block:: bash

    $ sudo usermod -aG docker $USER

Run the following command, if it doesn't work then reboot and run it again.

.. code-block:: bash

    $ newgrp docker

Check if docker can be run as non-root.

.. code-block:: bash

    $ docker run hello-world

Reboot if you got error.
