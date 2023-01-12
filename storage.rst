Storage: can I repair it or recover data from it ?
==================================================

There are 3 kinds of storage:

 * `Direct Attached Storage <https://en.wikipedia.org/wiki/Direct-attached_storage>`_ (DAS) or local storage for hard disks connected via

   *  IDE/PATA
   *  SATA/eSATA
   *  SAS
   *  firewire
   *  devices connected via USB (external disk, digital camera, thumb drive, phone...) in USB mass storage mode

 * `Storage Area Networks <https://en.wikipedia.org/wiki/Storage_area_network>`_ (SAN)

   * Fibre Channel Protocol (FCP)
   * Fibre Channel over Ethernet (FCoE)
   * iSCSI, mapping of SCSI over TCP/IP

 * `Network Attached Storage <https://en.wikipedia.org/wiki/Network-attached_storage>`_ (NAS)

   *  Windows share (CIFS/SMB)
   *  Network File System (NFS)
   *  Phone or digital camera in Media Transfer Protocol (MTP) mode (even if connected via USB)


TestDisk & PhotoRec can recover data from DAS and SAN storage. For NAS server (QNAP, Synology...), they need to run on the server itself or the disks need to be moved to a computer running Linux (sometimes FreeBSD).
TestDisk & PhotoRec can store recovered data on any storage available from your computer. When recovering deleted files, be careful to avoid writing new data to the same partition the files were stored on.

