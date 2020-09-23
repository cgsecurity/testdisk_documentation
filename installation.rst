Installation
============

Linux: Installation of distribution package
*******************************************
CentOS
------
As root,

.. code-block:: none

   yum install testdisk qphotorec

Fedora
------
As root,

.. code-block:: none

   dnf install testdisk qphotorec

Fedora Copr
-----------
Copr is an automatic build system. It provide the latest development version.
As root,

.. code-block:: none

   dnf copr enable grenier/testdisk
   dnf install testdisk qphotorec

Debian / Ubuntu
---------------
As root,

.. code-block:: none

   apt install testdisk

macOS
---------------
Install brew from https://brew.sh if you haven't do so:

.. code-block:: none

   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

Then, install testdisk

.. code-block:: none

   brew install testdisk

Official binaries
*****************
Official binaries: stable or WIP ?
----------------------------------

Using the development version (WIP=Work In Progress) is usually recommended as fixes are not backported.
The WIP archive may be modified several times per week but keep the same name. If this version doesn't start,
you can always use the stable version and warn the developer of the problem with the beta version.

Installation of official binaries for Windows
---------------------------------------------

 * Download the archive (32-bit x86 or 64-bit x64) from https://www.cgsecurity.org/wiki/TestDisk_Download
 * Extract all the files including the subdirectories

Installation of official binaries for macOS
-------------------------------------------

Download the archive from https://www.cgsecurity.org/wiki/TestDisk_Download

   * macOS / Mac OS X Intel / OS X
   * Mac OS X PowerPC for very old Mac (Mac OS X <= 10.5)

Extract all the files including the subdirectories

Installation of official binaries for Linux
-------------------------------------------

Download the archive from https://www.cgsecurity.org/wiki/TestDisk_Download
Currently we have

 * https://www.cgsecurity.org/testdisk-7.1.linux26-x86_64.tar.bz2 for the last stable version
 * https://www.cgsecurity.org/testdisk-7.2-WIP.linux26-x86_64.tar.bz2 for the development version

The archives contains static binaries for Intel (x86_64 or i686) platforms. They should work as-is on any
recent Linux distribution.

Decompress the archive, no need to be root

.. code-block:: none

   tar xjf testdisk-7.1-WIP.linux26-x86_64.tar.bz2


List your files, a directory named :file:`testdisk-7.2-WIP` should has been created.
