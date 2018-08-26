SMART status - Disk health monitoring
=====================================
The smartmontools package contains two utility programs (smartctl and smartd) to control and monitor storage systems using the Self-Monitoring, Analysis and Reporting Technology System (SMART) built into most modern ATA/SATA, SCSI/SAS and NVMe disks. In many cases, these utilities will provide advanced warning of disk degradation and failure.

This package is installed by default on most Linux distribution. For Windows and macOS, there are respectively a setup.exe and an dmg available from https://sourceforge.net/projects/smartmontools/files/smartmontools/


.. code-block:: none

   sudo smartctl -a /dev/sda
   === START OF INFORMATION SECTION ===
   Model Family:     Western Digital Green
   Device Model:     WDC WD20EZRX-00D8PB0
   Serial Number:    WD-WMC4M0875073
   LU WWN Device Id: 5 0014ee 058f9952c
   Firmware Version: 80.00A80
   User Capacity:    2,000,398,934,016 bytes [2.00 TB]
   Sector Sizes:     512 bytes logical, 4096 bytes physical
   Device is:        In smartctl database [for details use: -P show]
   ATA Version is:   ACS-2 (minor revision not indicated)
   SATA Version is:  SATA 3.0, 6.0 Gb/s (current: 6.0 Gb/s)
   Local Time is:    Mon Oct  3 13:16:17 2016 CEST
   SMART support is: Available - device has SMART capability.
   SMART support is: Enabled
   
   === START OF READ SMART DATA SECTION ===
   SMART overall-health self-assessment test result: PASSED
   ...
   SMART Attributes Data Structure revision number: 16
   Vendor Specific SMART Attributes with Thresholds:
   ID# ATTRIBUTE_NAME          FLAG     VALUE WORST THRESH TYPE      UPDATED  WHEN_FAILED RAW_VALUE
     5 Reallocated_Sector_Ct   0x0033   200   200   140    Pre-fail  Always       -       0


Even if the SMART health status is `PASSED`, it doesn't mean the disk is OK. You should also check the "Reallocated_Sector_Ct" attribute.

When the hard drive finds a read/write/verification error, it marks that sector as "reallocated" and transfers data to a special reserved area (spare area). This process is also known as remapping, and reallocated sectors are called "remaps". The raw value normally represents a count of the bad sectors that have been found and remapped. Thus, the higher the attribute value, the more sectors the drive has had to reallocate. This allows a drive with bad sectors to continue operation; however, a drive which has had any reallocations at all is significantly more likely to fail in the near future. While primarily used as a metric of the life expectancy of the drive, this number also affects performance. As the count of reallocated sectors increases, the read/write speed tends to become worse because the drive head is forced to seek to the reserved area whenever a remap is accessed. If sequential access speed is critical, the remapped sectors can be manually marked as bad blocks in the file system in order to prevent their use.

I recommend to replace a harddisk when the first bad sectors appears.

