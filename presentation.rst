Presentation
============

TestDisk & PhotoRec are free and open-source data recovery utilities.
TestDisk has been created in 1998 and PhotoRec in April 2002 by Christophe GRENIER, they can be downloaded from https://www.cgsecurity.org/.
They are distributed under the GNU General Public License v2 or later, you can

 * run the program as you wish, for any purpose,
 * study how the program works, and change it so it does your computing as you wish (You have access to the source code.),
 * redistribute copies so you can help your neighbor,
 * distribute copies of your modified versions to others under the same license. By doing this you can give the whole community a chance to benefit from your changes.

This documentation can be found online at https://github.com/cgsecurity/testdisk_documentation.
Anyone can contribute to TestDisk & PhotoRec documentation. We especially welcome the contributions of beginners. In fact, beginners have a distinct advantage over the experts, because they can more easily spot the places where documentation is lacking. If it's only to fix a spelling or grammar error, your contribution is also welcome!

Archives with ready-to-use binaries are available for

 * DOS (32-bit x86)
 * Microsoft Windows (32-bit x86 or 64-bit x64)
 * Linux (32-bit x86 or 64-bit x64)
 * Mac OS X (PowerPC or Intel) / OS X / macOS
 * Marvell 88F628x Linux

TestDisk & PhotoRec can also be compiled for other platforms, notably

 * FreeBSD/OpenBSD/NetBSD, Unix-like computer operating system descended from Berkeley Software Distribution (BSD), a Research Unix derivative developed at the University of California, Berkeley.
 * Haiku, a free and open-source operating system compatible with the now discontinued BeOS.
 * SunOS/Solaris, a Unix-branded operating system developed by Sun Microsystems for their workstation and server computer systems,


TestDisk - Partition recovery
*****************************

TestDisk recognizes the following disk partitioning:

 * Apple partition map
 * GUID Partition Table
 * Humax
 * PC/Intel Partition Table (master boot record)
 * Sun Solaris slice
 * Xbox fixed partitioning scheme

It also handles non-partitioned media.

TestDisk can

 * recover deleted partition
 * rebuild partition table
 * rewrite the Master boot record (MBR)

TestDisk does a quick check of the disk's structure and compares it with the partition table for entry errors.
Next, it searches for lost partitions of these file systems:

 * Be File System (BeOS)
 * BSD disklabel (FreeBSD/OpenBSD/NetBSD)
 * Cramfs, Compressed File System
 * DOS/Windows FAT12, FAT16, and FAT32
 * Windows exFAT
 * HFS, HFS+ and HFSX, Hierarchical File System
 * IBM Journaled File System 2 (JFS2)
 * Linux ext2, ext3 and ext4
 * Linux RAID

   * RAID 1: mirroring
   * RAID 4: striped array with parity device
   * RAID 5: striped array with distributed parity information
   * RAID 6: striped array with distributed dual redundancy information

 * Linux Swap (versions 1 and 2)
 * LVM and LVM2, Linux Logical Volume Manager
 * Novell Storage Services (NSS)
 * Windows New Technology File System (NTFS)
 * ReiserFS 3.5, 3.6 and 4
 * Sun Solaris i386 disklabel
 * Unix File System UFS and UFS2 (Sun/BSD/…)
 * XFS, SGI’s Journaled File System


TestDisk - Filesystem repair
****************************

TestDisk can deal with some specific logical filesystem corruption:

 * File Allocation Table, FAT12 and FAT16

   * Find filesystem parameters to rewrite a valid boot sector
   * Use the two copies of the FAT to rewrite a coherent version

 * File Allocation Table, FAT32

   * Find filesystem parameters to rewrite a valid boot sector
   * Restore the boot sector using its backup
   * Use the two copies of the FAT to rewrite a coherent version

 * exFAT

   * Restore the boot sector using its backup

 * NTFS (New Technology File System) boot sector and MFT repair

   * Find filesystem parameters to rewrite a valid boot sector
   * Restore the boot sector using its backup
   * Restore the Master File Table (MFT) from its backup

 * Extended file systems, ext2, ext3 and ext4

   * Find backup superblock location to assist fsck

 * HFS+

   * Restore the boot sector using its backup

TestDisk - File recovery
************************
When a file is deleted, the list of disk clusters occupied by the file is erased, marking those sectors available for use by other files created or modified thereafter. If the file wasn't fragmented and the clusters haven't been reused, TestDisk can recover the deleted file for various filesystem:

 * FAT
 * NTFS
 * exFAT
 * ext2

PhotoRec - File recovery
************************
PhotoRec is a file carver data recovery software tool. It doesn't recover the original filenames but it can recover delete files even from corrupted filesystem.
PhotoRec recognizes and recovers numerous file formats including ZIP, Office, PDF, HTML, JPEG and various graphics file formats. The whole list of file formats recovered by PhotoRec contains more than 480 file extensions (about 300 file families). It's possible to create custom signature to recover file format unknown to PhotoRec.

QPhotoRec - File recovery
*************************
QPhotoRec is a file carver data recovery software tool with a graphical user interface. Like PhotoRec, it doesn't recover the original filenames but it can recover delete files even from corrupted filesystem.

