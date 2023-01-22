TestDisk and PhotoRec in various digital forensics test cases
=============================================================

PhotoRec is considered one of the best file carving utilities for several reasons:

  * File format support: PhotoRec is able to recover a wide range of file types, including photos, videos, documents, and music files. It can also recover files from various file systems, including NTFS, exFAT, FAT, and ext2/ext3/ext4.
  * Robustness: PhotoRec is able to recover files even if the file system is severely damaged or the storage device has been reformatted. It can also recover files that have been deleted or lost due to formatting or other errors.
  * Flexibility: PhotoRec is a command-line tool, which gives users more control and flexibility in how they recover files. It also includes a graphical user interface called QPhotoRec, which makes it easy for users who are less familiar with command-line interface.
  * Open-source : PhotoRec is open source software. That means users can see the code, make changes and contribute to the development of the software.
  * Free: PhotoRec is completely free to use, which makes it accessible to a wide range of users and organizations.

All these factors make PhotoRec an extremely powerful and versatile file carving utility that can be used to recover a wide range of files from various storage devices.

The Computer Forensics Tool Testing (CFTT) program is a program run by the National Institute of Standards and Technology (NIST), which is a U.S. federal agency that provides technical standards and guidelines for a variety of industries and organizations, including forensic science.
PhotoRec has been evaluated by the CFTT in 2014 for Forensic `File Carving purpose <https://www.nist.gov/itl/ssd/software-quality-group/computer-forensics-tool-testing-program-cftt/cftt-technical-0>`_. PhotoRec had the best results ;-)

It's worth noting that while Photorec is a widely used tool in forensic investigations, it's not the only one, and it may not be the best one for some cases. Other tools may be more appropriate for specific types of investigations or for specific types of storage media. The choice of the appropriate tool will depend on the specific needs of the investigation and the technical expertise of the forensic investigator.

To learn to use TestDisk and PhotoRec, various test cases are available to practice in safe conditions.

.. toctree::

   dftt_fat16_undelete
   dftt_ntfs_undelete
   dfrws2006
   forensics
