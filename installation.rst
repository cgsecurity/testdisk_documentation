Installation
============

Linux: Installation of distribution package
*******************************************

Arch Linux
----------
TestDisk is available in the Extra repo from `Arch Linux <https://www.archlinux.org>`_.
As root,

.. code-block:: none

   pacman -S testdisk


CentOS
------

TestDisk and QPhotoRec are available in the EPEL repository for `CentOS <https://www.centos.org>`_.
As root,

.. code-block:: none

   yum install epel-release
   yum install testdisk qphotorec

If epel repository is disabled on your CentOS, use

.. code-block:: none

   yum install --enablerepo=epel testdisk qphotorec


Debian
------

TestDisk is available for `Debian <https://debian.org>`_.

As root,

.. code-block:: none

   apt update
   apt install testdisk

Fedora
------

TestDisk is available for `Fedora <https://www.fedoraproject.org>`_.

As root,

.. code-block:: none

   dnf install testdisk qphotorec

Fedora Copr
-----------

`Copr <https://copr.fedorainfracloud.org/>`_ is an automatic build system for Fedora. It provide the latest development version.
As root,

.. code-block:: none

   dnf copr enable grenier/testdisk
   dnf install testdisk qphotorec

Gentoo
------

TestDisk is available on `Gentoo <https://www.gentoo.org>`_.

.. code-block:: none

   sudo emerge --ask app-admin/testdisk

openSUSE
--------

.. code-block:: none

   zypper refresh
   zypper install testdisk photorec qphotorec

Ubuntu
------
As root on the `Ubuntu <https://www.ubuntu.com>`_ system,

.. code-block:: none

   apt update
   apt install testdisk

macOS: Installation via Homebrew
********************************

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

   * macOS / Mac OS X Intel / OS X 32-bit (Mac OS X <= 10.14)
   * Mac OS X PowerPC for very old Mac (Mac OS X <= 10.5)

Extract all the files including the subdirectories

Currently there is no official binaries for macOS 64-bits, so for macOS Catalina (10.15) and Big Sur (10.16),
see `macOS: Installation via Homebrew`_

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

   tar xjf testdisk-7.2-WIP.linux26-x86_64.tar.bz2


List your files (:command:`ls`), a directory named :file:`testdisk-7.2-WIP` should has been created in the current working directory.
