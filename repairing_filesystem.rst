Repairing filesystem
====================

Repairing a filesystem may be a risky business as sometimes the problem is "fixed" by removing all invalid files.
So if you have access to some of your files but not all, it's recommended to backup what it's possible to access before trying to repair the filesystem.

Repairing filesystems from Windows
----------------------------------

Windows can read and write files from FAT, exFAT and NTFS filesystem. The :command:`chkdsk` command is used to check and repair filesystems.
Run :command:`cmd` (Right-click Run As Administrator)

.. code-block:: none

   chkdsk /f d:


Repairing filesystems from Linux
--------------------------------

Linux can read and write from a large variety of filesystems. The :command:`fsck` generic command is used to run a filesystem check.
To check and repair automatically the filesystem on /dev/sda, run as root

.. code-block:: none

   fsck -y /dev/sda1

fsck starts a filesystem specific command, in example for ext4, it run :command:`fsck.ext4`.
If you need a fine grained repair, you should read the man page of the command related to the filesystem you want to repair, i.e. :command:`man fsck.ext4`.
If some files or directories are missing, remember to check the :file:`lost+found` directory at the root of this filesystem.

:command:`ntfsfix` can be used to repair NTFS filesystem followed by Windows :command:`chkdsk` . Note that it resets the NTFS journal file, so it should be used only if Windows failed to repair the filesystem.

Repairing filesystems from macOS
--------------------------------
To check an external drive,

.. code-block:: none

   sudo diskutil list
   sudo fsck /dev/disk1s1

You may have to repeat the :command:`fsck` command several times until no remaining error is reported.

If you get Invalid b-tree node size, you can try

.. code-block:: none

   sudo fsck_hfs -r -d /dev/disk1s1

Repairing FAT32, exFAT and NTFS boot sector using TestDisk
----------------------------------------------------------
The boot sector is a sector containing information required to access any files from a FAT, exFAT or NTFS filesystem.
FAT32 and NTFS filesystems have a main boot sector and a backup. If the main boot sector is damaged, the filesystem is listed as raw or unreadable.
TestDisk is able to use the backup boot sector to repair the main boot sector:

 * start TestDisk
 * select the device containing the partition (avoid drive letter like D:)
 * confirm the partition table type
 * go in the Advanced menu
 * select the partition
 * choose Boot

If the boot sector is damaged, *Boot sector: Bad* will be shown.
If the backup is OK, *Backup boot sector: Ok* will also be listed.

* choose BackupBS
* confirm
* Quit
* restart the computer


TestDisk: Repairing FAT boot sector
-----------------------------------

The first sector of a FAT filesystem is named boot sector. It contains the main filesystem properties and some small code necessary only to start the computer from this partition.
If the boot sector is damaged, it's impossible to access your data. Windows :command:`chkdsk` or Linux :command:`fsck` can not repair a filesystem without a valid boot sector, they return error message like *Chkdsk is not available for RAW drives*. Fortunately TestDisk can find all the parameters that need to be recorded in the boot sector and rewrite this sector, so further repair operations or normal access can be conducted.

 * start TestDisk
 * select the device containing the partition (avoid drive letter like D:)
 * confirm the partition table type
 * go in the Advanced menu
 * select the FAT partition
 * choose Boot
 * select RebuildBS
 * choose List

If testdisk is able to list your files, choose

  * quit the file listing
  * choose Write
  * confirm
  * Quit
  * restart the computer

.. _repairing_ntfs_boot_sector:

TestDisk: Repairing NTFS boot sector
------------------------------------

The first sector of a NTFS filesystem is named boot sector. It contains the main filesystem properties and some small code necessary only to start the computer from this partition.
If the boot sector is damaged, it's impossible to access your data. Windows :command:`chkdsk` or Linux :command:`fsck` can not repair a filesystem without a valid boot sector, they return error message like *Chkdsk is not available for RAW drives*. Fortunately TestDisk can find all the parameters that need to be recorded in the boot sector and rewrite this sector, so further repair operations or normal access can be conducted.

 * start testdisk
 * select the device containing the partition (avoid drive letter like D:)
 * confirm the partition table type
 * go in the Advanced menu
 * select the NTFS partition
 * choose Boot
 * select RebuildBS
 * choose List

If testdisk is able to list your files, choose

  * quit the file listing
  * choose Write
  * confirm
  * Quit

TestDisk: repairing ext2/3/4 filesystem superblock
--------------------------------------------------

1024 bytes after the beginning of the ext2/3/4 filesystem sits the superblock. It contains the main filesystem properties.
With a damaged main superblock, it's not possible to mount and access the files normally. Fortunately copies of the main superblock are spread over the filesystem. To be precise, they are not exact copy of the main superblock, each copy contains its own location to prevent confusion between copies and the original. TestDisk can search for alternate superblocks.

 * start testdisk
 * select the device containing the partition
 * confirm the partition table type
 * go in the Advanced menu
 * select the Linux partition
 * choose SuperBlock


.. code-block:: none

   TestDisk 7.1-WIP, Data Recovery Utility, August 2016
   Christophe GRENIER <grenier@cgsecurity.org>
   http://www.cgsecurity.org
   
   Disk /dev/sda - 2000 GB / 1863 GiB - CHS 243201 255 63
   
        Partition                  Start        End    Size in sectors
   
     MS Data                     2048 3907020799 3907018752 [/home2]
   superblock 0, blocksize=4096 [/home2]
   superblock 32768, blocksize=4096 [/home2]
   superblock 98304, blocksize=4096 [/home2]
   superblock 163840, blocksize=4096 [/home2]
   superblock 229376, blocksize=4096 [/home2]
   superblock 294912, blocksize=4096 [/home2]
   superblock 819200, blocksize=4096 [/home2]
   superblock 884736, blocksize=4096 [/home2]
   superblock 1605632, blocksize=4096 [/home2]
   superblock 2654208, blocksize=4096 [/home2]
   
   To repair the filesystem using alternate superblock, run
   fsck.ext4 -p -b superblock -B blocksize device

   >[  Quit  ]
                               Return to Advanced menu

If superblock 0 is listed, it means the main superblock is correct. If it's damaged, this line will be missing,
use next superblock and block size information to run :command:`fsck`.

.. code-block:: none

   fsck.ext4 -p -b 32768 -B 4096 /dev/sda1

Repairing HFS/HFS+ volume header using TestDisk
-----------------------------------------------

The volume header is locate 1024 bytes after the beginning of the HFS/HFS+ filesystem. If it is damaged, it is not possible to access files normally.
TestDisk is able to use the backup volume header to repair the main volume header:

 * start TestDisk
 * select the device containing the partition
 * confirm the partition table type
 * go in the Advanced menu
 * select the partition
 * choose SuperBlock

If the main superblock is damaged, *Volume header: Bad* will be shown.
If the backup is OK, *Backup volume header: HFS+ Ok* (or HFS Ok) will also be listed.
In this case,

* choose BackupBS
* confirm
* Quit
* restart the computer

Repairing BitLocker volume
--------------------------

:command:`Repair-bde` can reconstruct critical parts of the drive and salvage recoverable data as long as a valid recovery password or recovery key is used to decrypt the data.
See https://technet.microsoft.com/en-us/library/ff829851(v=ws.11).aspx
