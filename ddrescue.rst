DDRescue: data recovery from damaged disk
=========================================

A bad sector is a sector on a computer's disk drive that is either inaccessible or unwriteable due to permanent damage, such as physical damage to the disk surface.
Flash memory may also have "bad sectors" (even if technically there is no sector in flash memory) due to permanent damage like failed flash memory transistors.

Instead of working directly on the damaged disk, it's recommended to create a copy and to work on the clone.
Two possibilities: create a disk image (a file) or overwrite a new/empty disk.

ddrescue can be found for Linux or macOS. If your computer is using another operating system, no problem, create a Linux LiveUSB! (See :ref:`live-usb`)

ddrescue on Linux
*****************
drescue is available on all Linux distribution.

 * CentOS: ``yum install ddrescue``
 * Debian/Ubuntu: ``apt install gddrescue``
 * Fedora: ``dnf install ddrescue``

Use ``lsblk`` or ``testdisk -lu`` to identify all the disks.

ddrescue on macOS
*****************
To install ddrescue:

 * Press Command+Space and type ``Terminal`` and press enter/return key.
 * Run in Terminal app:

.. code-block:: none


   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install ddrescue

Done! You can now use ``ddrescue``.
Use ``diskutil list`` to get information on all available disks and their partitioning.

DDRescue: disk to file image
****************************
It's the recommended method for forensic purpose.
You need enough space to store the file: if you want to create a clone of a 1TB disk, you need at least 1TB free on a filesystem.
Avoid FAT filesystem for the destination as they are limited to 4GB file.

In the following example, an image named sdb.dd will be created from the second disk /dev/sdb.

.. code-block:: none

   ddrescue /dev/sdb sdb.dd sdb.log

The log file ``sdb.log`` can be used to restart the recovery.
It can take a few hours to several days to clone a disk with a lot of bad sectors.

DDRescue: disk to disk copy
***************************
The destination disk must be at least as big as the original one. Be careful, two disks of the same announced capacity from different vendors or sometimes from different models of the same vendor can differ slightly in size (a few 100 MB).

Ie. WD10EZRZ and WD10EZEX are two models sold by Western Digital as 1TB model, in fact the first one is 1,000,000 MB, the second one 1,000,204 MB.

Before beginning, disconnect all disks, usb device, cd/dvd reader/writer not needed: there is less chance to overwrite the wrong disk.

.. code-block:: none

   ddrescue /dev/sdb /dev/sdc sdb.log

The log file ``sdb.log`` can be used to restart the recovery.


ddrutility: restricting ddrescue to NTFS allocated data block
*************************************************************
When a disk contains a lot of bad sectors, it may be safer to use `ddrutility <https://sourceforge.net/projects/ddrutility/>`_ to limit the copy to allocated data block from an NTFS partition.

.. code-block:: none

   testdisk -lu /home/kmaster/data/data_for_testdisk/ntfs.dd
   TestDisk 7.1-WIP, Data Recovery Utility, August 2016
   Christophe GRENIER <grenier@cgsecurity.org>
   http://www.cgsecurity.org
   Please wait...
   Disk /dev/sdb - 130 MB / 124 MiB - CHS 16 255 63 (RO)
   Sector size:512
   
   
   Disk /dev/sdb - 130 MB / 124 MiB - CHS 16 255 63 (RO)
        Partition			Start        End    Size in sectors
    1 * HPFS - NTFS                   32     255487     255456 [NTFS]
        NTFS, blocksize=512

In this example, the first NTFS partition begins at sector 32 and the sector size is 512 bytes.

.. code-block:: none

   ddru_ntfsbitmap /dev/sdb -i $((32 * 512)) sdb1_domain
   ddrescue /dev/sdb sdb.dd sdb.log -m sdb1_domain


