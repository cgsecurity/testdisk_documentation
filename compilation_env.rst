Compilation environment
***********************
TestDisk uses several libraries if available:

 * libncurses - Required, TestDisk and PhotoRec use a text user interface, Ncurses library and development files must be available.
 * Ext2fs library - Optional, used by TestDisk to list files from ext2/ext3/ext4 partition and by PhotoRec to be able to carve the free space from an ext2/ext3 partition instead of the whole partition
 * EWF library - Optional, TestDisk and PhotoRec use it to access Expert Witness Compression Format files (e.g. Encase files)
 * Iconv - Optional, used to handle Unicode filenames
 * Jpeg library - Optional, used by PhotoRec to improved JPEG recovery rate
 * NTFS library - Optional, used by TestDisk to list files from NTFS partition
 * Reiserfs library - Optional, used by TestDisk to list files from reiserfs partition
 * zlib library - Optional, used by PhotoRec to decompress gzipped content
 * Qt5 library - Optional, required for QPhotoRec and to update the configure script.

Linux
-----

 * Debian/Ubuntu:
   :command:`apt-get install build-essential e2fslibs-dev libewf-dev libncurses5-dev libncursesw5-dev ntfs-3g-dev libjpeg-dev uuid-dev zlib1g-dev qtbase5-dev qttools5-dev-tools pkg-config dh-autoreconf git`
 * RHEL/CentOS 6 or later:
   :command:`yum install @buildsys-build desktop-file-utils e2fsprogs-devel libewf-devel libjpeg-devel libuuid-devel ncurses-devel ntfs-3g-devel qt-devel qt5-qtbase-devel zlib-devel git`
 * Fedora:
   :command:`dnf install @buildsys-build desktop-file-utils e2fsprogs-devel libewf-devel libjpeg-devel libuuid-devel ncurses-devel ntfs-3g-devel qt-devel qt5-qtbase-devel zlib-devel git`

macOS
-----
Install Xcode

.. code-block:: none

   xcode-select --install

Install brew

.. code-block:: none

   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

Install pkg-config, libjpeg-turbo and wget via brew

.. code-block:: none

  brew install pkg-config libjpeg-turbo wget


Download wanted library (Adjust the version)

.. code-block:: none

  wget -N http://prdownloads.sourceforge.net/e2fsprogs/e2fsprogs-1.46.2.tar.gz
  wget -N https://download.tuxera.com/opensource/ntfs-3g_ntfsprogs-2017.3.23.tgz
  wget -N https://www.cgsecurity.org/testdisk-7.2-WIP.tar.bz2

Decompress and compile them (Replace :file:`/User/kmaster` by the correct path)

.. code-block:: none

  tar xzf e2fsprogs-1.46.2.tar.gz
  tar xzf ntfs-3g_ntfsprogs-2017.3.23.tgz
  tar xzf testdisk-7.2-WIP.tar.bz2
  cd e2fsprogs-1.46.2 && ./configure && make && cd ..
  cd ntfs-3g_ntfsprogs-2017.3.23 && ./configure --disable-ntfs-3g --disable-nfconv && make && cd ..
  mkdir -p testdisk
  ../testdisk-7.2-WIP/configure  --disable-qt \
    --with-ext2fs-lib=/Users/kmaster/e2fsprogs-1.46.2/lib \
    --with-ext2fs-includes=/Users/kmaster/e2fsprogs-1.46.2/lib \
    --with-ntfs3g-lib=/Users/kmaster/ntfs-3g_ntfsprogs-2017.3.23/libntfs-3g/.libs/ \
    --with-ntfs3g-includes=/Users/kmaster/ntfs-3g_ntfsprogs-2017.3.23/include/ \
    --with-jpeg-lib=/usr/local/opt/jpeg-turbo/lib \
    --with-jpeg-includes=/usr/local/opt/jpeg-turbo/include
  make
  cd ..

Windows
-------
cygwin
^^^^^^
Cygwin https://cygwin.com/ is a large collection of GNU and Open Source tools which provide functionality similar to a Linux distribution on Windows, it includes the GCC compiler.
A DLL (:file:`cygwin1.dll`) provides substantial POSIX API functionality, such functions may be required by some libraries that TestDisk or PhotoRec can use.

MinGW-w64
^^^^^^^^^
MinGW-w64 https://www.mingw-w64.org/ is a free and open source software development environment for creating Microsoft Windows applications. It provides GCC for Windows 64 & 32 bits.
