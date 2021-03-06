Z shell
=======

The Z shell or zsh is an interactive UNIX shell and a powerful command-line
interpreter for scripting languages, including shell scripting. The Z-Shell
has become one of the most popular shells for the Linux operating system.
It is rich in features and easy to configure and customize.

Install
-------

Update the package repository cache of your Ubuntu 20.04 LTS operating system
and then install ZSH.

.. code-block:: bash

    $ sudo apt-get update
    $ sudo apt-get install zsh

Now set ZSH as the default login shell for the user you’re logged in as with the following command.

.. code-block:: bash

    $ sudo usermod -s /usr/bin/zsh $(whoami)

And restart your machine.

.. code-block:: bash

    $ sudo reboot

Open up a terminal after your computer boots and press the number key ``2``.
ZSH should create a new ``~/.zshrc`` configuration file.

Plugins
-------

Powerline is a status line plugin for ZSH shell. Powerline font lets the ZSH shell
use different icons and symbols on the shell.

.. code-block:: bash

    $ sudo apt-get install powerline fonts-powerline

ZSH has a Syntax Highlighting plugin that you can install from the official package repository.
Run the following command to install ZSH Syntax Highlighting Plugin.

.. code-block:: bash

    $ sudo apt-get install zsh-syntax-highlighting

Oh-My-ZSH
---------

ZSH has an entire framework Oh-My-ZSH dedicated to work with Git.
To learn more about Oh-My-ZSH, take a look at the official GitHub page at
https://github.com/robbyrussell/oh-my-zsh

To install Oh-My-ZSH, run the following command:

.. code-block:: bash

    $ sudo apt install curl
    $ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

Now run the following command to enable ZSH Syntax Highlighting plugin installed earlier:

.. code-block:: bash

    $ echo "source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc

Autosuggestions
---------------

Download zsh-autosuggestions with the following command:

.. code-block:: bash

    $ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

Open ``~/.zshrc`` and uncomment the following line:

.. code-block:: bash

    # plugins=(git)

and replace it by the following one:

.. code-block:: bash

    plugins=(git zsh-autosuggestions)

Changing Default Theme
----------------------

Download ``powerlevel10k`` theme using following command:

.. code-block:: bash

    $ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k

And run the following command to enable it:

.. code-block:: bash

    $ echo 'source ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k/powerlevel10k.zsh-theme' >>! ~/.zshrc

Finally restart the shell.
