Recovering deleted partition using TestDisk
===========================================

When a partition is deleted or if the partition table is corrupted, the filesystems remain on the disk but their location is unknown and no data can be accessed.
TestDisk can search partitions and rewrite the partition table with the partitions selected by the user.

Start testdisk
--------------

* :ref:`running_testdisk_win`
* :ref:`running_testdisk_linux`
* :ref:`running_testdisk_macos`

Log creation
------------

 * Choose Create unless you have a reason to append data to the log or if you execute TestDisk from read only media and can't create it elsewhere.
 * Press Enter to proceed.

.. note::  Windows users, if you have difficulties to find the :file:`testdisk.log` file, consult https://support.microsoft.com/en-us/kb/865219 on how to show file name extensions in Windows Explorer.

Disk selection
--------------
All hard drives should be detected and listed with the correct size by TestDisk.

 * Use up/down arrow keys to select your hard drive with the lost partition/s.
 * Press Enter to Proceed.

.. note:: macOS - If available, use raw device :file:`/dev/rdisk*` instead of :file:`/dev/disk*` for faster data transfer.

.. warning:: Windows - Do not select :file:`C:`, :file:`D:` or another drive letter. It's useless to search partitions inside a partition.

Partition table type selection
------------------------------
TestDisk displays the partition table types.
 * Select the partition table type - usually the default value is the correct one as TestDisk auto-detects the partition table type.
 * Press Enter to Proceed.

Analyze current partition table
-------------------------------

 * Select **Analyse**
 * Confirm with the Enter key
 * TestDisk will list the current partition table.

If a partition is damaged or a partition entry corrupted, the problem will be listed and the partition listed twice.
By example, if you see "Invalid NTFS or exFAT boot" on a partition (partition size is OK, the partition doesn't overlap another one...) you want to access, it's better to fix this problem (
:ref:`repairing_ntfs_boot_sector`) before searching other partitions.

 * Confirm at **Quick Search** to proceed


Quick Search for partitions
---------------------------

TestDisk displays the first results in real time. If necessary, you can choose Stop to abort the quick search.
TestDisk lists all partitions it has found.
To list the files of a FAT, exFAT, NTFS, ext2/3/4 filesystem, highlight this partition and press **P**. Press **Q** to return to the partition list.

Search for more partitions
--------------------------

If a partition is still missing, choose **[Deeper Search]**. It can take a few hours, so you need to be certain that your computer will not sleep (Power management feature...)

Partitions selection
--------------------

Partitions listed as D(eleted) will not be recovered if you let them listed as deleted.
Use the arrow keys to switch the partitions you want to recover (check the partition size, list the file contents...) from D(eleted) to \*(bootable), P(rimary) or L(ogical).
Only one partition can be listed as \*(bootable). It is not a problem if a partition is marked as bootable on a disk you will not start from (e.g. an external disk) but there MUST be a bootable partition on a disk you want to start your computer from.

Once all the partitions you want to keep and all the partitions you want to recover are properly marked as non deleted, continue on next screen.
Review the partitions list. If all partitions are listed and only in this case, confirm at Write with Enter, y and OK.
Now, the partitions are registered in the partition table.

If a FAT32 or an NTFS partition was found using its backup boot sector, TestDisk will let you rewrite the main boot sector with the content of the backup boot sector: to copy the backup of the boot sector over the boot sector, select Backup BS, validate with Enter, use y to confirm.

Restart your computer.
