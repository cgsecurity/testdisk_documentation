How to make the system bootable again
*************************************

Check that

 * all partitions are listed in the partition table
 * a partition with your computer OS is listed as \*(bootable)
 * you can list the files from the bootable partition


DOS - Window 95/98
------------------

If your OS doesn't boot, you can reinstall the system files with :command:`sys c:`.

Windows 2000/XP/2003
--------------------

 * Run :command:`fixmbr` from the Recovery Console

.. code-block:: none

   fixmbr \Device\HardDisk0

If you still have the problem,

 * Run :command:`fixboot` to repair NTFS boot sector.
 * Check :file:`c:\\boot.ini` content

Windows Vista/Windows 7/..., Windows Server 2008/...
----------------------------------------------------
 * Run :command:`bootrec.exe /fixmbr` from the Recovery Console
 * For legacy / PC Intel partition table, check :file:`c:\\boot.ini` content
 * For EFI GPT, check the output of :command:`bcdedit /v`. To modify the settings, use the :command:`bcdedit /set` command.
 * Run :command:`bootrec.exe /fixboot` to repair NTFS boot sector.

Linux/FreeBSD
-------------

 * Update your :file:`/etc/fstab` to reflect the new partition order.
 * Update your multiboot configuration

    * Lilo: :file:`/etc/lilo.conf`
    * Grub: :file:`/boot/grub/grub.conf`
    * Grub2: :file:`/etc/grub2-efi.cfg`

 * Reinstall the multiboot in the Master Boot Record.

.. code-block:: none

   lilo
   grub-install device
   grub2-install device


