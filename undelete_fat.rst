TestDisk: undelete file for FAT, exFAT, ext2
********************************************

FAT is mainly used on memory cards from digital cameras and on USB keys.
When a file is deleted, the filename is marked as deleted and the data area as unallocated/free, but TestDisk can read the deleted directory entry and find where the file began. If the data area hasn't been overwritten by a new file, the file is recoverable.

exFAT can be found on large memory card, large USB keys and hard disk.

ext2 is a Linux filesystem. It has been superseded by ext3 and ext4, so it's not found often now.
With ext3 and ext4, it's possible to find the names of the deleted files but the location of the deleted data isn't available anymore, so even if ext3/ext4 is similar to ext2, it's not possible to recover lost files using TestDisk.

Start testdisk
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

macOS If available, use raw device ``/dev/rdisk*`` instead of ``/dev/disk*`` for faster data transfer.

Partition table type selection
------------------------------
TestDisk displays the partition table types.
 * Select the partition table type - usually the default value is the correct one as TestDisk auto-detects the partition table type.
 * Press Enter to Proceed.

Start the undelete process
--------------------------
 * Select **Advanced**
 * Select the partition that was holding the lost files and choose **Undelete**

File undelete
-------------
Navigate to the folder where your files were.
Deleted files and directories are displayed in red.

 * To undelete a file, select the file to recover and press 'c' to copy the file.
 * To recover a deleted directory, select the directory and press 'c' to undelete the directory and its content.

Select where recovered files should be written
----------------------------------------------
Select the destination

File recovery is completed
--------------------------
When you get your files back, use Quit to exit.

If testdisk has been unable to find your lost data, try PhotoRec instead.
