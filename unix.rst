Linux / macos / BSD command line
********************************

The command line is a text interface to your computer/your NAS. It is often referred to as the shell, terminal, console, prompt.
This short guide will give you a few basic commands and concepts.

Starting a terminal
-------------------

To open a Terminal

* if your computer is actually running Linux with a Gnome graphical interfaces:

  * Choose "Activities" on the top left
  * On the prompt "type to search", type :command:`Terminal`
  * Click on the "Terminal" icon

* if your computer is running macox

  * Press Command+Space and type :command:`Terminal` and press enter/return key.
  * Run in Terminal app

* if your computer is running Windows and you want to connect to your NAS by ssh

  * use a ssh client like Putty

* if your computer is running Linux or macos and you want to connect to your NAS by ssh

  * Press Command+Space and type :command:`Terminal` and press enter/return key.
  * Run in Terminal app
  * :command:`ssh root@192.168.0.1` (Replace root if necessary and 192.168.0.1 by the correct IP)


Users
-----

The root user is the default privileged user. Usually, the terminal prompt ends by '#' for root and by '$' for the other users.
To check the current user, use :command:`id`.
To become root from an user account, you can try

 * :command:`sudo -s` You may be prompted for your user password.
 * :command:`su -` You may have to type the root password.

There will be no echo when you type the password.

Filesystem
----------

* Filenames, paths and commands are case-sensitives. You need to respect the upper "ABC" and lower "abc" cases.
* All files accessible in a Unix system are arranged in one big tree, the file hierarchy, rooted at :file:`/`.
* The root user have access to every files, directories and commands [#]_.
* The :command:`mount` command serves to attach the filesystem found on some device to the big file tree.
* Conversely, the :command:`umount` command will detach it again.
* When using a graphical interface, mount and umount operations can be done by a few mouse clicks on the icons representing the device.
* When using the command line, root privileges are required.
* The mount point is the name of the directory where the device is attached. By convention, it's usually in :file:`/mnt`, :file:`/media` or :file:`/run/media`.

.. [#] Root access may be restricted by Role-Based Access Control (RBAC), Multi-Level Security (MLS)...

Commands
--------

* :command:`cd directory_name`: change current directory
* :command:`pwd`: print working directory
* :command:`ls`: list files from current directory (files beginning by a dot are not listed by default)
* :command:`./testdisk_static`: lanch the testdisk_static program assuming it is present in the current directory.
* :command:`testdisk`: launch testdisk if the command is found in the PATH, a list of directories. It will not try to start a programmed name testdisk in the correct directory.
