# Dell Inspiron Laptop Setup

## Disable touchscreen

To disable the touchscreen input permanently, find your touchscreen XID and
add disable it.

```
$ xinput --list
# Lists your devices

$ xinput disable 12
```

Open your startup applications.

```
$ gnome-session-properties
```

Click Add and enter the `disable` command to be executed at login (name and comment are optional).

## Change close lid action

Open the /etc/systemd/logind.conf file in a text editor as root.

```
$ sudo gedit /etc/systemd/logind.conf
```

Change the line

```
#HandleLidSwitch=ignore
```

To this line:

```
HandleLidSwitch=hibernate
```

And restart service.

```
$ sudo service systemd-logind restart
```
