OpenConnect
===========

To install OpenConnect, run the following command from the command line:

.. code-block:: bash

    $ sudo apt install openconnect

Try to connect to the VPN server using the following command:

.. code-block:: bash

    $ sudo openconnect <vpn-server> --user <username>

You will be prompted to enter your password. After entering your password, you will be connected to the VPN server.

If you run into the issues, do the following to fix it.

Edit ``/etc/ssl/openssl.cnf`` as a sudoer to enable legacy provider.
It should look like this:

.. code-block:: text

    [openssl_init]
    providers = provider_sect

    # List of providers to load
    [provider_sect]
    default = default_sect
    legacy = legacy_sect
    # The fips section name should match the section name inside the
    # included fipsmodule.cnf.
    # fips = fips_sect

    # If no providers are activated explicitly, the default one is activated implicitly.
    # See man 7 OSSL_PROVIDER-default for more details.
    #
    # If you add a section explicitly activating any other provider(s), you most
    # probably need to explicitly activate the default provider, otherwise it
    # becomes unavailable in openssl.  As a consequence applications depending on
    # OpenSSL may not work correctly which could lead to significant system
    # problems including inability to remotely access the system.
    [default_sect]
    activate = 1

    [legacy_sect]
    activate = 1

Try to connect again. It should now hopefully work. If it doesn't you might need to perform a couple of extra steps.

In ``/usr/local/etc`` create a file names ``legacy_openssl.cnf`` and add the following content:

.. code-block:: text

    openssl_conf = openssl_init

    [openssl_init]
    ssl_conf = ssl_sect

    [ssl_sect]
    system_default = system_default_sect

    [system_default_sect]
    Options = UnsafeLegacyRenegotiation

Locate the directory which contains the ``openconnect`` csd wrapper scripts.
It can be e.g. ``/usr/libexec/openconnect``. There are usually two scripts ``csd-post.sh`` and ``csd-wrapper.sh``.

Edit both scripts to add this at the top of the scripts.

.. code-block:: bash

    export OPENSSL_CONF=/usr/local/etc/legacy_openssl.cnf

Hopefully, OpenConnect should now work.

To start OpenConnect from the command line, run the following command:

.. code-block:: bash

    $ sudo openconnect <vpn-server> --user <username> --csd-wrapper /usr/libexec/openconnect/csd-post.sh --no-external-auth --userAgent=AnyConnect -b

This will start OpenConnect in the background.

To stop it, simply find a corresponding process ID and kill it.

.. code-block:: bash

    $ ps aux | grep openconnect
    $ sudo kill -9 <pid>
