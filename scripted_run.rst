Scripted run
============
TestDisk and PhotoRec can run automatically using their own built-in commands. A script file (such as .cmd or .bat batch files under MS-DOS/Windows, or some shell under Linux) may also be helpful.

Automating recovery using TestDisk
**********************************
Syntax:

.. code-block:: none

   testdisk [/debug] [/log] [/logname file.log] /cmd [file.dd|file.e01|device] cmd

Some examples
-------------

.. code-block:: none

   testdisk /debug /log /cmd /dev/hda analyze,search
   testdisk /debug /log /cmd partition.dd partition_none,geometry,H,32,analyze,list,advanced,boot,rebuildbs,list


Device selection
----------------
Use the device name, e.g. `/dev/hda`, `/dev/hdb`, `/dev/sda`.

For DOS version, use `/dev/sda128` for first disk, `/dev/sda129` for the second and so on...
You may have to use single quote, i.e. ``'c:\input dir\image.dd'``, if the path or file name contains spaces.
For Encase files, you can use ``file.e??`` if you have less than 100 files, otherwise use ``file.???``

Partition type selection
------------------------

 * partition_i386
 * partition_gpt
 * partition_humax
 * partition_mac
 * partition_none
 * partition_sun
 * partition_xbox
 * ask_type: the user will be asked for the partition type (new in 6.9)

If no partition type is specified or asked, TestDisk will detect it automatically.

Main menu
---------

 * advanced
 * analyze
 * delete
 * geometry
 * mbr_code
 * options
 * list

Analyse menu
------------

 * backup: save to backup.log file the current partition structure
 * number: select a partition found during Quick Search or Deeper Search
 * list: list of the content of the selected partition (first one by default, new in 6.10)
 * search: Deeper Search for more partitions
 * noconfirm,write
 * write

Advanced menu
-------------

 * type
 * addpart: add a partition entry (not written to disk)
 * boot: for FAT12/FAT16, FAT32, exFAT and NTFS partition, go to the specific menu
 * copy: backup the partition to the file image.dd (new in 6.9)
 * list: list the content of the partition (new in 6.10)
 * list,recursive: list the content of the whole partition (new in 6.10)
 * list,recursive,fullpathname: list the content of the whole partition with the whole pathname (new in 6.11)
 * list,filecopy: list and copy all the files (new in 7.1)
 * superblock: search ext2/ext3 superblocks or go to HFS+ menu depending of the partition
 * undelete: go in the undelete menu (FAT12/16/32, NTFS, exFAT, ext2)
 * number: the partition number to select

Add partition
^^^^^^^^^^^^^

 * PC Intel

   * c,XX starting cylinder
   * h,XX starting head
   * s,XX starting sector
   * C,XX ending cylinder
   * H,XX ending head
   * S,XX ending sector
   * T,XX type

 * EFI GPT, Mac, XBoX

   * s,XX	starting sector
   * s,XX ending sector
   * T,XX type

 * Humax, Sun

   * c,XX starting cylinder
   * C,XX ending cylinder
   * T,XX type

FAT12/FAT16 boot menu
^^^^^^^^^^^^^^^^^^^^^

 * dump
 * list (new in 6.9)
 * list,recursive: list the contents of the whole partition (new in 6.10)
 * list,recursive,fullpathname: list the contents of the whole partition with the whole path name (new in 6.11)
 * rebuildbs
 * repairfat
 * initroot

FAT32 boot menu
^^^^^^^^^^^^^^^
 * dump
 * list (new in 6.9)
 * list,recursive: list the contents of the whole partition (new in 6.10)
 * list,recursive,fullpathname: list the contents of the whole partition with the whole path name (new in 6.11)
 * rebuildbs
 * repairfat
 * originalfat
 * backupfat

FAT rebuild menu
^^^^^^^^^^^^^^^^
 * list
 * list,recursive: list the contents of the whole partition (new in 6.10)
 * dump
 * noconfirm,write
 * write

exFAT boot menu
^^^^^^^^^^^^^^^
 * dump
 * originalexFAT
 * backupexFAT

NTFS boot menu
^^^^^^^^^^^^^^
 * rebuildbs
 * dump
 * list
 * list,recursive: list the contents of the whole partition (new in 6.10)
 * list,recursive,fullpathname: list the contents of the whole partition with the complete path name (new in 6.11)
 * originalntfs
 * backupntfs
 * repairmft
 * noconfirm,backupntfs
 * noconfirm,repairmft

NTFS undelete menu
^^^^^^^^^^^^^^^^^^
 * allundelete (new in 7.1): list and recover all deleted files. WARNING: stores them in current local directory.

NTFS rebuild menu
^^^^^^^^^^^^^^^^^
 * list
 * list,recursive: list the contents of the whole partition (new in 6.10)
 * list,recursive,fullpathname: list the contents of the whole partition with the complete path name (new in 6.11)
 * dump
 * noconfirm,write
 * write

HFS+ superblock menu
^^^^^^^^^^^^^^^^^^^^
 * dump
 * originalhfsp
 * backuphfsp

Geometry menu
-------------

 * C,number of cylinders
 * H,number of heads
 * S,number of sectors
 * N,sector size

Options
-------

 * dump
 * nodump
 * align
 * noalign
 * expert
 * noexpert

Automating recovery using PhotoRec
**********************************

.. code-block:: none

   photorec [/debug] [/log] [/logname file.log][/d recup_dir] [/cmd <device> <command>]

General syntax:

 * /debug: switch on debug mode
 * /log: switch on logging (a log file named :file:`photorec.log` will be created/appended to in the current working directory
 * /logname file.log: log will be written to :file:`file.log` instead of :file:`photorec.log`
 * /d recup_dir: specify directory to store the recovered files into. This should be on a device different from the one you are recovering from. PhotoRec will add a numeric extension to the path specified, starting with ".1" - and increase this number as long as a directory with this name already exists.
 * /cmd: introduces the command section for scripted run
 * <device>: the device (or image file) to recover from (Hint: use single-quote if the image file contains spaces)
 * <command>: the command list (see below)

Some examples of data recovery using PhotoRec
---------------------------------------------

Recover from the second IDE drives i386 partition the user selects

.. code-block:: none

   photorec /debug /log /cmd /dev/hdb partition_i386,select,search
 

Recover from the first IDE drives i386 partition #5, which is using ext2/ext3/ext4

.. code-block:: none

   photorec /debug /log /cmd /dev/hda partition_i386,options,mode_ext2,5,search


Recover from a given disk image file named :file:`disk.dmp` which only has a single ext4 partition (or a part of it)
Restore all file types known to PhotoRec to ``/mnt/recover/disk``.

.. code-block:: none

   photorec /debug /log /d /mnt/recover/disk /cmd disk.dmp options,mode_ext2, \
     fileopt,everything,enable,search
   
The same without debug and log - but recover only :file:`*.gif` and :file:`*.jpg`

.. code-block:: none

   photorec /d /mnt/recover/disk /cmd disk.dmp options,mode_ext2,fileopt,everything,disable, \
     jpg,enable,gif,enable,search
   
Recover jpg from the freespace of the first partition

.. code-block:: none

   photorec /cmd /dev/hda fileopt,everything,disable,jpg,enable,freespace,search


Recover all files from freespace from each partition as detected by TestDisk

.. code-block:: none

   PARENT=`pwd`
   DEVICE=/dev/sda
   testdisk -l $DEVICE | tee testdisk.log | \
     egrep "[[:digit:]][[:space:]][P,E,L,D,*][[:space:]].+([[:space:]]+[[:digit:]]+){3}" | \
     cut -f 2 -d\  |while read PARTITION
   do
     mkdir $PARTITION && cd $PARTITION &&
     xterm -e photorec /log /debug /d ./ /cmd $DEVICE freespace,$PARTITION,search
     cd $PARENT
   done


Command list
------------
Below you find a list of available command options, grouped into categories. It is best to use them in the order they are mentioned here.
These options must be separated by a comma. Partition type selection and options from the main menu can be used directly.

PhotoRec - Partition type selection
-----------------------------------

 * partition_i386
 * partition_gpt
 * partition_humax
 * partition_mac
 * partition_none
 * partition_sun
 * partition_xbox
 * ask_type: the user will be asked for the partition type

If no partition type is specified, it is auto-detected.

PhotoRec - Main menu
--------------------

 * fileopt: change file types to recover
 * inter: PhotoRec usage becomes interactive
 * options
 * number: the partition number to select
 * blocksize: force the block size - followed by the block size in bytes.
 * geometry
 * wholespace / freespace : files will be recovered from the whole partition or only from the free space (new in 6.10)
 * ext2_group: carve the group whose number is following (new in 6.10)
 * ext2_inode: carve the group whose following inode belongs to (new in 6.10)
 * search: start the recovery

PhotoRec - fileopt menu
-----------------------

 * everything,enable: use the values by default (may be different than the saved values, new in 6.9)
 * everything,disable: empty the list of file formats to locate (new in 6.9)
 * jpg,enable: will search for jpg
 * jpg,disable: will not search for jpg

You can use the same syntax for all file formats.

PhotoRec - Options menu
-----------------------

To use anything from the options menu, you must specify the keyword "options" first.

 * expert
 * keep_corrupted_file_no (new in 6.10)
 * keep_corrupted_file
 * paranoid_no / paranoid / paranoid_bf (new in 6.10)
 * lowmem
 * mode_ext2

Windows UAC
***********

If you run TestDisk and PhotoRec, Windows User Account Control will ask "Do you want the following program from an unknown publisher to make changed to this computer ?" (or something similar). As administrator rights are unneeded for disk images, you may want to avoid this UAC prompt with the ``__COMPAT_LAYER`` environment variable. Example:

.. code-block:: none

   set __COMPAT_LAYER=RunAsInvoker
   photorec_win.exe /cmd image.dd search
