IDE
===

This instruction shows how to install several IDEs.

JetBrains Toolbox App
---------------------

First, we install JetBrains Toolbox App that we will use for managing JetBrains IDEs.
Download the installer executable from the `Toolbox App web page <https://www.jetbrains.com/toolbox-app/>`__
and run the installer.

.. code-block:: bash

    $ sudo tar -xzf jetbrains-toolbox-2.3.1.31116.tar.gz -C /opt/
    $ cd /opt/jetbrains-toolbox-2.3.1.31116/
    $ ./jetbrains-toolbox

Log in to your JetBrains Account from the Toolbox App, and it will automatically activate the available
licenses for any IDE that you install.

Add path to the Toolbox App executable to your PATH environment variable:

.. code-block:: bash

    $ echo 'export PATH="$HOME/.local/share/JetBrains/Toolbox/scripts:$PATH"' >> ~/.zshrc
    $ source ~/.zshrc

PyCharm via JetBrains Toolbox
-----------------------------

After you run the Toolbox App, click its icon in the notification area and select which product you want to install.
In our case, we will install PyCharm Professional.

Test the installed PyCharm IDE by creating a new project. If it crashes, you can run it
from the terminal to see the error message.

.. code-block:: bash

    $ cd .local/share/JetBrains/Toolbox/apps/pycharm-professional/bin/
    $ ./pycharm.sh

Last time I got the following error:

.. code-block:: text

    The SUID sandbox helper binary was found, but is not configured correctly.
    Rather than run without sandboxing I'm aborting now.
    You need to make sure that chrome-sandbox is owned by root and has mode 4755.

At the moment, I don't know how to fix it properly. The following workaround works for me:

.. code-block:: bash

    $ sudo chown root:root $HOME/.local/share/JetBrains/Toolbox/apps/pycharm-professional/jbr/lib/chrome-sandbox
    $ sudo chmod 4755 $HOME/.local/share/JetBrains/Toolbox/apps/pycharm-professional/jbr/lib/chrome-sandbox

WebStorm via JetBrains Toolbox
------------------------------

The installation of WebStorm is similar to PyCharm. Just select WebStorm from the Toolbox App.
After the installation, run it from the terminal to see if it works.

.. code-block:: bash

    $ cd .local/share/JetBrains/Toolbox/apps/webstorm/bin/
    $ ./webstorm.sh

Try to open an existing project or create a new one. If IDE crashes with the following error:

.. code-block:: text

    The SUID sandbox helper binary was found, but is not configured correctly.
    Rather than run without sandboxing I'm aborting now.
    You need to make sure that chrome-sandbox is owned by root and has mode 4755.

Apply the same workaround as for PyCharm.

.. code-block:: bash

    $ sudo chown root:root $HOME/.local/share/JetBrains/Toolbox/apps/webstorm/jbr/lib/chrome-sandbox
    $ sudo chmod 4755 $HOME/.local/share/JetBrains/Toolbox/apps/webstorm/jbr/lib/chrome-sandbox
