Recovering lost videos from a memory card using PhotoRec
========================================================

Due to the way videos are recorded, all videos created by some digital camera (i.e. Canon 5D Mark III) are fragmented on the memory card. Data recovery software, photorec included, expect non fragmented files.

If all videos (.mov / .mp4) recovered by PhotoRec are unreadable, you are probably in this case. Note this chapter does not concern copies or downloaded files, only files written by some digital camera, not by your computer.

When using PhotoRec, in FileOpts, enable

.. code-block:: none

    [X] mov/mdat Recover mdat atom as a separate file

and next start the recovery.

If you sort the files by name, you should see that the names alternates between _ftyp.mov and _mdat.mov.
You need to concatenate each ftyp file with a mdat file:

* If using Windows, run ``cmd`` to start a terminal, use ``cd directory_name`` to go where your files are, and run

.. code-block:: none

   type file2_ftyp.mov file1_mdat.mov > test.mov

If you do not have the permissions to write to the directory, before using the type command, take ownership of the directories or run ``cmd`` using right click run as administrator.

* Under macOS and Linux, start a terminal/console, use ``cd directory_name`` to go where your files are, and run


.. code-block:: none

   cat file2_ftyp.mov file1_mdat.mov > test.mov

f you do not have the permissions to write to the directory, before using the cat command, change the files and directories ownership using ``chown -R username:groupname recup_dir.*``

Play the resulting test.mov file. If it works, you need to do the same with each couple of files.

This solution works only for videos written in two fragments. Videos from GoPro HD2, Hero3-Black Edition, HERO4 Silver are stored in more than 2 fragments, so special software solutions are needed to recover such videos. This chapter does not concern copies or downloaded files, only files written by some digital camera, not by your computer.
