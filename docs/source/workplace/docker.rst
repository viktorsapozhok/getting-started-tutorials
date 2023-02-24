Docker
======

Docker is an open platform for developing, shipping, and running applications.
Docker enables you to separate your applications from your infrastructure
so you can deliver software quickly.

Docker Engine
-------------

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

Docker Compose
--------------

Compose is a tool for defining and running multi-container Docker applications.
With Compose, you use a YAML file to configure your application’s services.
Then, with a single command, you create and start all the services from your configuration.

Read `here <https://docs.docker.com/compose/install/linux/>`__ about the installation.

To download and install the Compose CLI plugin, run:

.. code-block:: bash

    $ DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
    $ mkdir -p $DOCKER_CONFIG/cli-plugins
    $ curl -SL https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose

.. note::

    To install a different version of Compose, substitute 2.16.0 with the version of Compose you want to use.

Apply executable permissions to the binary.

.. code-block:: bash

    $ chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose

Test the installation.

.. code-block:: bash

    $ docker compose version
    Docker Compose version v2.16.0

Run docker as a non-root user
-----------------------------

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
