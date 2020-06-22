Starting the tools
==================


Disk image
**********

TestDisk and PhotoRec can be used on disk image:

 * raw files (.dd)
 * Encase (.E01)
 * splitted Encase files (.E01, E02...)

Splitted raw files are not supported.
No administrator rights are needed to run :command:`testdisk` or :command:`photorec` on disk image.

Examples:

 * :command:`photorec image.dd` to carve a raw disk image
 * :command:`photorec image.E01` to recover files from an Encase EWF image
 * :command:`photorec 'image.???'` if the Encase image is split into several files.

.. _running_testdisk_win:

Running TestDisk, PhotoRec or QPhotoRec under Windows
*****************************************************

Double-click on the executable (:command:`testdisk_win.exe`, :command:`photorec_win.exe` or :command:`qphotorec_win.exe`) from an account in the Administrator Group.
Administrator rights are necessary to get a low-level access to all medias (hard disk, USB key, Smart Card, etc.).
Windows UAC (Vista and later) will ask you to confirm that you want to run the executable with administrator rights.

.. note:: Windows users, if you see ``cygwin1.dll not found, c\\cygwin is missing``, extract all the files from the archive before running TestDisk or PhotoRec. 

.. _running_testdisk_linux:

Running TestDisk, PhotoRec under Linux
**************************************

You need to be root to run TestDisk.

.. code-block:: none

   cd testdisk-7.1
   sudo ./testdisk_static


.. code-block:: none

   cd testdisk-7.1
   sudo ./photorec_static

.. note:: If your Raid device (ie. Intel raid) is missing, run "sudo dmraid -ay" to activate it.

Running QPhotoRec under Linux X.org X11
***************************************

QPhotoRec is a Qt5 application, it isn't shipped with the official Linux binaries
from www.cgsecurity.org. But it is available on most Linux distribution or can be compiled from source.
To run it in a Terminal,

.. code-block:: none

   sudo qphotorec

Running QPhotoRec under Linux Wayland
*************************************

To run QPhotoRec in a Terminal,

.. code-block:: none

   xhost +local: 
   sudo qphotorec

.. _running_testdisk_macos:

Running TestDisk, PhotoRec under macOS
**************************************

If you are not root, TestDisk (i.e. :command:`testdisk-7.1/testdisk`) or PhotoRec will restart itself using :command:`sudo` after confirmation from your part.

If your administrator account has no password (a blank password), you must give that user a password before using the :command:`sudo` command:

- Choose Apple menu > System Preferences and click Accounts.
- Click Change Password.

Terminal doesn't show the password as you type. If you enter the wrong password or a blank password, the command isn't executed and Terminal asks you to try again.

.. _running_fidentify_win:

Running Fidentify under Windows
*******************************

Fidentify checks all the files from a directory with the same signatures than PhotoRec. It's useful to check if PhotoRec is able to recover some file extensions/some file formats.
Run :command:`cmd`, Windows Command Prompt. :command:`cd` is the command to change directory.

.. code-block:: none

   cd testdisk-7.1
   fidentify_win.exe d:\directory

.. _running_fidentify_linux:

Running Fidentify under Linux or macOS
**************************************

Start a terminal, go in :file:`testdisk` directory and use :command:`fidentify` to check if the files present in a directory are recognized. This identification is identical in PhotoRec.

.. code-block:: none

   cd testdisk-7.1
   ./fidentify_static /home/user/


