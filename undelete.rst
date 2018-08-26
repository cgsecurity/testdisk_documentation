Recovering deleted files using TestDisk
=======================================
When a file is deleted, the data remains on the disk. Unless new data has overwritten your lost file, TestDisk can usually recover it.
It's possible for

 * FAT12/16/32
 * exFAT
 * NTFS
 * ext2

For other filesystems or if sought-after lost files are still missing, give PhotoRec a try. PhotoRec is a signature based file recovery utility and may be able to recover your data where other methods failed.

* Do not further use the media (HDD, USB key, ...) on which the data stored have been deleted until data recovery process is completed.
* It is highly recommended that TestDisk or PhotoRec recovers files on another destination media, at minimum on another filesystem.

For maximum security, TestDisk doesn't try to unerase files but lets
you copy the deleted files onto another partition or disk. Remember, you must avoid
writing anything on the filesystem that was holding the data. If you do, 
deleted files may be overwritten by new ones.

.. toctree::
   undelete_fat.rst
   undelete_ntfs.rst

