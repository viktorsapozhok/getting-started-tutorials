Serve sphinx documentation with nginx in docker
===============================================

First, we need to pull nginx docker image:

.. code-block:: bash

    docker pull nginx:latest

Then we can run a basic web server using following:

.. code-block:: bash

    docker run -it --rm -d -p 8080:80 --name docs -v ~/proj/docs/build/html:/usr/share/nginx/html nginx

Where ``docs`` is a name of the container. 

Documentation is now available on http://localhost:8080/