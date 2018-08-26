Recovering deleted files using PhotoRec
=======================================

PhotoRec doesn't recover the original filenames or the file structure but it can recover lost files even from corrupted filesystem.
PhotoRec is a signature based file recovery utility (a file carver) and may be able to recover your data where other methods failed.

Remember, you must avoid writing anything on the filesystem that was holding the data. If you do, 
deleted files may be overwritten by new ones.

Start photorec
**************

* :ref:`running_testdisk_win`
* :ref:`running_testdisk_linux`
* :ref:`running_testdisk_macos`

Disk selection
**************
Available media are listed. Use up/down arrow keys to select the disk that holds the lost files.

 * Use up/down arrow keys to select your hard drive with the lost partition/s.
 * Press Enter to Proceed.

Hint for macOS: If available, use raw device ``/dev/rdisk*`` instead of ``/dev/disk*`` for faster data transfer.


Source partition selection
**************************
Choose
 * ``Search`` after selecting the partition that holds the lost files to start the recovery,
 * ``Options`` to modify the options,
 * ``File Opt`` to modify the list of file types recovered by PhotoRec.

PhotoRec options
****************
 * ``Paranoid`` By default, recovered files are verified and invalid files rejected. Enable ``bruteforce`` if you want to recover more fragmented JPEG files, note it is a very CPU intensive operation, it's started after the normal scan process.
 * The ``expert mode`` option allows the user to force the file system block size and the offset. Each filesystem has his own block size (a multiple of the sector size) and offset (0 for NTFS, exFAT, ext2/3/4), these value are fixed when the filesystem has been created/formatted. When working on the whole disk (i.e. original partitions are lost) or a reformatted partition, if PhotoRec has found very few files, you may want to try the minimal value that PhotoRec let you select (it's the sector size) for the block size (0 will be used for the offset).
 * Enable ``Keep corrupted files`` to keep files even if they are invalid in the hope that data may still be salvaged from an invalid file using other tools.
 * Enable ``Low memory`` if your system does not have enough memory and crashes during recovery. It may be needed for large file systems that are heavily fragmented. Do not use this option unless absolutely necessary.

Selection of files to recover
*****************************
In ``FileOpts``, enable or disable the recovery of certain file types, for example,

.. code-block:: none

   [X] riff RIFF audio/video: wav, cdr, avi
   ...
   [X] tif  Tag Image File Format and some raw file formats (pef/nef/dcr/sr2/cr2)
   ...
   [X] zip  zip archive including OpenOffice and MSOffice 2007

The whole list of file formats recovered by PhotoRec contains more than 300 file families representing more than 480 file extensions.

File system type
****************
Once a partition has been selected and validated with ``Search``, PhotoRec needs to know how the data blocks are allocated.
Unless it is an ext2/ext3/ext4 filesystem, choose ``Other``.

Carve the partition or unallocated space only
*********************************************

PhotoRec can search files

 * from the whole partition (useful if the filesystem is corrupted) or
 * from the unallocated space only (available for ext2/ext3/ext4, FAT12/FAT16/FAT32 and NTFS). With this option only deleted files are recovered.

Select where recovered files should be written
**********************************************
Choose the directory where the recovered files should be written. Use the arrow keys (up, down, left, right) to navigate, you can also use the enter key to enter into a directory.

 * Dos/Windows/Os2: To get the drive list (C:, D:, E:, etc.), use the arrow keys to select ``..``, press the ``Enter`` key - repeat until you can select the drive of your choice. Validate with ``Y`` es when you get the expected destination.
 * Linux: File system from external disk may be available in a ``/media``, ``/mnt`` or ``/run/media`` sub-directory. Mount your destination drive if necessary.
 * macOS: Partitions from external disk are usually mounted in ``/Volumes``.

.. warning:: Do not store the recovered files on the source filesystem. Otherwise lost data may be overwritten and definitively lost.

Recovery in progress
********************
Number of recovered files is updated in real time.
 * During pass 0, PhotoRec searches the first 10 files to determine the blocksize. This step is skipped when searching files from the unallocated space only, the blocksize value found in the filesystem structure is used.
 * During pass 1 and later, files are recovered including some fragmented files.

Recovered files are written in recup_dir.1, recup_dir.2... sub-directories. It's possible to access the files even if the recovery is not finished.

Recovery is completed
*********************
When the recovery is complete, a summary is displayed. Note that if you interrupt the recovery, the next time PhotoRec is restarted you will be asked to resume the recovery.

 * Thumbnails found inside pictures are saved as ``t*.jpg``
 * If you have chosen to keep corrupted files/file fragments, their filenames will beginning by the letter ``b`` (roken).
 * Windows: You may have disabled your live antivirus protection during the recovery to speed up the process, but it's recommended to scan the recovered files for viruses before opening them - PhotoRec may have undeleted an infected document or a Trojan.
 * Hint: When looking for a specific file. Sort your recovered files by extension and/or date/time. PhotoRec uses time information (metadata) when available in the file header to set the file modification time.

.. note:: Windows - You may need to take ownership of the recup_dir.* folders: https://technet.microsoft.com/en-us/library/Cc753659.aspx

.. note:: macOS / Linux - To change the owner of the files, run ``sudo chown -R username recup_dir.*``


PhotoRec: file name and date
****************************
By default, files are saved in directories named recup_dir.1, recup_dir.2...
A new directory is created each new 500 files (The thumb files are not included in this count, nor the report.xml file).
A filename begins by a letter followed by a number (7 digits or more) and ends, if any, by a file extension.

Letter meaning:

 * f=file
 * b=broken
 * t=jpeg embedded thumbnail

The number is calculated by using the file location minus the partition offset divided by the block size. For some filesystems like NTFS, exFAT, ext2/3/4, this number may be identical to the original cluster/block number.
Using metadata information embedded in the recovered file, the file may be renamed to include the documentation title (example, Microsoft Office doc/xls/ppt or Acrobate pdf files) like
``recup_dir.1/f0016741_Prudent_Engineering_Practice_for_Cryptographic_Protocols.pdf``.

By default, the file creation and modification times are corresponding to the data recovery time. Some file format may embedded date/time information (ie. jpg pictures taken by a digital camera, Microsoft Office documents), PhotoRec will try to reuse them. This way, it may be easier to sort the recovered files. For forensics purpose, do not trust this information blindly: the date/time information may be off by a few hours (no or wrong timezone information) or totally wrong (the original device clock may have a wrong date/time setting.)

