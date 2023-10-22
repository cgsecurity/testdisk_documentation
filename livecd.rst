.. _live-usb:

Creating a live USB
===================
If you need to repair a computer that isn't booting correctly, you can move its harddisk to a working computer or start your computer from an USB key or a DVD.
It's this later solution that will be presented here.

You need an USB flash drive also known as USB stick, thumb drive, pen drive, or jump drive that you can erase.
Note it's also possible to use a blank DVD.

Download Fedora "Image Live" from https://fedoraproject.org/fr/workstation/download/


Windows
-------

 *  Download and run `Rawrite32 <http://www.netbsd.org/~martin/rawrite32/>`_
 *  Choose the Fedora image as the **Filesystem image** - if the image file is not shown, you may have to change the file selector options or change the image's extension
 *  Choose the USB stick as the **Target**
 *  Double-check you're really, really sure you don't need any of the data on the USB stick!
 *  Click **Write to disk...**
 *  Wait for the operation to complete,

Linux (command line)
--------------------

 * Identify the name of the USB drive partition 
 * unmount all mounted partition from that device (Replace /run/media/user/mountpoint by the correct mountpoint)
 * use `dd` to create do the copy (Adapt the source and destination)

.. code-block:: none

   lsblk
   umount /run/media/user/mountpoint
   sudo dd if=/path/to/image.iso of=/dev/sdX bs=8M status=progress oflag=direct

Wait until the command completes.
If you receive ``dd: invalid status flag: ‘progress’ error``, your dd version doesn't support ``status=progress`` option and you'll need to remove it (and you won't see writing progress). 

.. warning:: The :command:`dd` command is very powerful and can destroy any existing data on the specified device.
   Make **absolutely sure** of the device name to write to and do not mistype the device name when using :command:`dd`!

Linux (GNOME)
-------------

This method is for people running Linux with GNOME, Nautilus and the GNOME Disk Utility installed. A standard installation of Fedora, or a standard GNOME installation of many other distributions, should be able to use this method. On Fedora, ensure the packages nautilus and gnome-disk-utility are installed. Similar graphical direct-write tools may be available for other desktops.

 *  Download a Fedora image, choose a USB stick that does not contain any data you need, and connect it
 *  Run Nautilus (Files) - for instance, open the Overview by pressing the Start/Super key, and type *Files*, then hit enter
 *  Find the downloaded image, right-click on it, go to **Open With**, and click **Disk Image Writer**
 *  Double-check you're really, really sure you don't need any of the data on the USB stick!
 *  Select your USB stick as the **Destination**, and click **Start Restoring...**
 *  Wait for the operation to complete, then reboot your computer, and do whatever you need to do to boot from a USB stick - often this will involve pressing or holding down **F12**, **F2** or **Del**.

OS X
----
 
 *  Open a terminal
 *  Run :command:`diskutil list`. This will list all disks connected to the system, as :file:`/dev/rdisk1`, :file:`/dev/rdisk2` and so on. Identify - very carefully! - which one corresponds to the USB stick you wish to use as destination. Hereafter, we'll assume it was :file:`/dev/rdisk2`` - modify the commands as appropriate for your stick.
 *  Run :command:`diskutil unmountDisk /dev/rdisk2`
 *  Type :command:`dd if=`, then drag and drop the Fedora image file to the terminal window - this should result in its filesystem location being appended to the command. Now complete the command with :command:`of=/dev/rdisk2 bs=1m`, but *don't hit Enter yet*. You should wind up with something like :command:`sudo dd if=/Volumes/Images/Fedora-Live-Desktop-x86_64-20-1.iso of=/dev/rdisk2 bs=1m`
 *  Double-check you have the correct disk number and you're really, really sure you don't need any of the data on the USB stick!
 *  Hit Enter

Starting from the USB stick
---------------------------
Plug the USB key on the damaged computer and boot this computer, and do whatever you need to do to boot from a USB stick - often this will involve pressing or holding down **F12**, **F2** or **Del**.
If you are using a Mac computer, hold down the left Alt/Option key to access the boot menu - you should see a Fedora logo. Click this to boot.

Original source of this page: https://docs.fedoraproject.org/en-US/quick-docs/creating-and-using-a-live-installation-image/index.html
