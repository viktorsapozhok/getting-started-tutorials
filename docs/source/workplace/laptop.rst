Custom laptop settings
======================

Disable touchscreen
-------------------

To disable the touchscreen input permanently, find your touchscreen XID and disable it.

.. code-block:: bash

    $ xinput --list
    # Lists your devices

    $ xinput disable [XID]

Open your startup applications.

.. code-block:: bash

    $ gnome-session-properties

Click Add and enter the ``disable`` command to be executed at login (name and comment are optional).

Change close lid action
-----------------------

Open the ``/etc/systemd/logind.conf`` file in a text editor as root.

.. code-block:: bash

    $ sudo gedit /etc/systemd/logind.conf

Change the line

.. code-block:: bash

    #HandleLidSwitch=ignore

To this line:

.. code-block:: bash

    HandleLidSwitch=hibernate

And restart service.

.. code-block:: bash

    $ sudo service systemd-logind restart

Fixing no sound issue
---------------------

This no sound fix works if your computer is using the ``snd_hda_intel`` kernel module.
So before attempting to apply this fix, check out to see if the ``snd_hda_intel``
kernel module is in use. For this you can run:

.. code-block:: bash

    $ lspci -nnk | grep -A2 Audio

Which should display the audio devices along with the kernel module / driver in use.
This is the output:

.. code-block:: bash

    00:1f.3 Audio device [0403]: Intel Corporation Cannon Lake PCH cAVS [8086:a348] (rev 10)
        Subsystem: Lenovo Cannon Lake PCH cAVS [17aa:2297]
        Kernel driver in use: snd_hda_intel
    --
    01:00.1 Audio device [0403]: NVIDIA Corporation TU104 HD Audio Controller [10de:10f8] (rev a1)
        Subsystem: Lenovo TU104 HD Audio Controller [17aa:2297]
        Kernel driver in use: snd_hda_intel
        Kernel modules: snd_hda_intel

If you do get ``snd_hda_intel`` in the output of the above commands, and you get
no sound (and only a Dummy Output) in Ubuntu, here's what you can try to fix it.
You need to add options ``snd-hda-intel model=generic`` at the end of the
/etc/modprobe.d/alsa-base.conf file.

.. warning::

    Do not modify anything else in this file!

You can add options ``snd-hda-intel model=generic`` at the end of
/etc/modprobe.d/alsa-base.conf by running this command:

.. code-block:: bash

    $ echo "options snd-hda-intel model=generic" | sudo tee -a /etc/modprobe.d/alsa-base.conf

Only run this command once because it adds this line each time you run it!
After this, reboot the system.
