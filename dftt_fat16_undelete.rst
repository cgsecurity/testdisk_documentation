DFTT: Undelete files from a FAT16 filesystem
********************************************

Download the small `FAT filesystem <https://sourceforge.net/projects/dftt/files/Test%20Images/6_%20FAT%20File%20Recovery%20%231/>`_ image archive and extract all the files.
This test image is a 6MB FAT16 file system with six deleted files and two deleted directories. The files range from single cluster files to multiple fragments.

To undelete all files manually,

 * run `testdisk 6-fat-undel.dd`
 * Choose `Proceed`.
 * A non partitioned media is detected automatically, press Enter to confirm.
 * Choose `Undelete`.

All files and directories are deleted, they are listed in red.

 * Press 'a' to select all files.

The selected files and directories are now listed in green and prefixed by '*' or '<' for the current highlighted file.

 * Press 'C' (uppercase) to copy all selected files and directories.
 * Choose a destination to copy all the files: use the arrow keys (up, down, left, right) to navigate, you can also use the enter key to enter into a directory.
 * Press 'C' when the destination is correct.

All files are copied.

 * Press 'q' to quit
 * Choose [Quit] until you have exited all menus

The usual filenames for a FAT filesystem are composed of 8 chars for the name and 3 for the extension.
When a file is deleted, the first character of the filename is overwritten. TestDisk represents the lost char by a underscore `_` (e.g. `_RAG1.DAT` instead of `FRAG1.DAT`)
If a long filename (> 8 characters) is present, it will be use instead. A benefit is that the whole filename can be displayed (e.g. `System Volume Information`)

All files are recovered successfully except the 3 fragmented files.
The size of these 3 files is correct but the content is wrong. When a file is deleted, the linked list formed by the cluster numbers used by the file are marked as free in the FAT tables. TestDisk assumes there is no fragmentation but it's not the case here.

