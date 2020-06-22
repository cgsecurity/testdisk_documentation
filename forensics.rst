Forensics: write blockers
*************************

The content of a disk may be modified by simply connecting it to a computer:

 * LVM driver will sync two RAID1-like volumes if they are out of sync
 * Linux Raid and fake Raid will also resync the disks if they are out of sync
 * Auto-mounting of the filesystem will modify the last-mount date and the mount count
 * ext3 and ext4 will replay the journal if the filesystem is dirty.
 * The NTFS file system may attempt to commit or rollback unfinished transactions, and/or change flags on the volume to mark it as "in use".
 * The operating system will update the access time for any file accessed
 * Windows may create hidden folders for the recycle bin or saved hardware configuration
 * Virus infections or malware on the system used for analysis may attempt to infect the disk being inspected.
 * Auto-indexation of the files may creates new files on the disk

Forensic disk controllers or hardware write-blockers are most commonly associated with the process of creating a disk image, or acquisition, during forensic analysis. Their use is to prevent inadvertent modification of evidence. Protecting an evidence drive from writes during investigation is also important to counter potential allegations that the contents of the drive were altered during the investigation. Of course, this can be alleged anyway, but in the absence of technology to protect a drive from writes, there is no way for such an allegation to be refuted.

A hardware write-blocker prevents modifications from the computer but it doesn't prevent a disk from modifying itself (i.e. SMART status
updates in service area each time the device is powered-on.). It remains the best solution to prevent accidental modifications.

Without a hardware write blocker, it's still possible to reduce the risks of accidental modifications.
Using a Linux computer without graphical interface and without auto-mounting *may* be considered a good enough solution.

Under Linux, :command:`blockdev` or :command:`hdparm` can be used to switch a disk to read-only:

.. code-block:: none

   blockdev --setro /dev/sdb
   hdparm -r1 /dev/sdb

In practice, it doesn't work! TestDisk will open these devices in read-write.


Loopback device is a safer alternative:

.. code-block:: none

   losetup -r /dev/loop0 /dev/sdb
   testdisk /dev/loop0

This way TestDisk is forced to open the device in read-only.


Loopback can also be used to mount a filesystem in read-only:
.. code-block:: none

   losetup -r /dev/loop0 /dev/sdb
   partprobe /dev/loop0
   mkdir /mnt/p1
   mount -o ro /dev/loop0p1 /mnt/p1

