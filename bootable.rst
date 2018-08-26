How to make the system bootable again
*************************************

Check that

 * all partitions are listed in the partition table
 * a partition with your computer os is listed as \*(bootable)
 * you can list the files from the bootable partition


DOS - Window 95/98
------------------

If your OS doesn't boot, you can reinstall the system files with ``sys c:``.

Windows 2000/XP/2003
--------------------

 * Run fixmbr from the Recovery Console

.. code-block:: none

   fixmbr \Device\HardDisk0

If you still have the problem,

 * Run `fixboot` to repair NTFS boot sector.
 * Check ``c:\boot.ini`` content

Windows Vista/Windows 7/..., Windows Server 2008/...
----------------------------------------------------
 * Run ``bootrec.exe /fixmbr`` from the Recovery Console
 * For legacy / PC Intel partition table, check ``c:\boot.ini`` content
 * For EFI GPT, check the output of ``bcdedit /v``. To modify the settings, use the ``bcdedit /set`` command.
 * Run ``bootrec.exe /fixboot`` to repair NTFS boot sector.

Linux/FreeBSD
-------------

 * Update your /etc/fstab to reflect the new partition order.
 * Update your multiboot configuration

    * Lilo: /etc/lilo.conf
    * Grub: /boot/grub/grub.conf
    * Grub2: /etc/grub2-efi.cfg

 * Reinstall the multiboot in the Master Boot Record.

.. code-block:: none

   lilo
   grub-install device
   grub2-install device


