TestDisk: undelete file for NTFS
********************************

Start TestDisk
--------------

* :ref:`running_testdisk_win`
* :ref:`running_testdisk_linux`
* :ref:`running_testdisk_macos`

Log creation
------------

 * Choose Create unless you have a reason to append data to the log or if you execute TestDisk from read only media and can't create it elsewhere.
 * Press Enter to proceed.

Disk selection
--------------
All hard drives should be detected and listed with the correct size by TestDisk.

 * Use up/down arrow keys to select your hard drive with the lost partition/s.
 * Press Enter to Proceed.

macOS If available, use raw device :file:`/dev/rdisk*` instead of :file:`/dev/disk*` for faster data transfer.

Partition table type selection
------------------------------
TestDisk displays the partition table types.
 * Select the partition table type - usually the default value is the correct one as TestDisk auto-detects the partition table type.
 * Press Enter to Proceed.

Start the undelete process
--------------------------
 * Select **Advanced**
 * Select the partition that was holding the lost files and choose **Undelete**

NTFS file undelete
------------------
TestDisk scans MFT entries for deleted files. A list of NTFS deleted files found by TestDisk is displayed

* To recover a single file, highlight the file and press 'c' (lowercase) to copy it.
* To recover a several files, move the first file you want to recover, press ':' to select it, repeat the process for the others files, press 'C' (uppercase) to copy them

It's not visible in interface but it's possible to filter the results, press 'f' to add a filter.
Several filters can be added. To cancel all the filters, press 'r' (reset).

Select where recovered files should be written
----------------------------------------------
Select the destination

File recovery is completed
--------------------------
When the NTFS file recovery is finished, choose Quit to exit.

If TestDisk has been unable to find your lost data, try PhotoRec instead.
