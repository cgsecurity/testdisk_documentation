DFTT: Undelete files from a NTFS filesystem
*******************************************
Download the small `NTFS filesystem <https://sourceforge.net/projects/dftt/files/Test%20Images/7_%20NTFS%20File%20Recovery%20%28and%20Leap%20Year%29%20%231/>`_ image archive and extract all the files. This test image is a 6MB NTFS file system with eight deleted files, two deleted directories, and a deleted alternate data stream. The files range from resident files, single cluster files, and multiple fragments. No data structures were modified in this process to thwart recovery. They were created in Windows XP, deleted in XP, and imaged in Linux.

To undelete all files manually,

 * run `testdisk 7-ntfs-undel.dd`
 * Choose `Proceed`.
 * A non partitioned media is detected automatically, press Enter to confirm.
 * Choose `Undelete`.

TestDisk lists all lost files successfully. The alternate data stream is listed as `./mult1.dat:ADS`, alternate streams are not listed in Windows Explorer, and their size is not included in the file's size. Malware has used alternate data streams to hide code. As a result, malware scanners and other special tools now check for alternate data streams. Forensics analyst should also search for them as they may be used to hide documents.

 * Press 'C' (uppercase) to copy all selected files and directories.
 * Choose a destination to copy all the files: use the arrow keys (up, down, left, right) to navigate, you can also use the enter key to enter into a directory.
 * Press 'C' when the destination is correct.

All files are copied.

 * Press 'q' to quit
 * Choose [Quit] until you have exited all menus

