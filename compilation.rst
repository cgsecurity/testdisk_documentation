Compilation
***********

Compilation from source archive
-------------------------------
Once you have downloaded the source archive from https://www.cgsecurity.org/wiki/TestDisk_Download, run

.. code-block:: none

   tar xjf testdisk-7.2-WIP.tar.bz2
   cd testdisk-7.2-WIP
   ./configure && make


Compilation from git repository
-------------------------------

.. code-block:: none

   git clone https://git.cgsecurity.org/testdisk.git

If you have already cloned the project, to update your local copy, run :command:`git pull` from the :file:`testdisk` directory. 

.. code-block:: none

   cd testdisk
   mkdir config
   autoreconf --install -W all -I config
   ./configure
   make


Compiling a static version
--------------------------
Once you have been able to build a "normal" version, you can try to build a static version.

.. code-block:: none

   make static


A `static build <https://en.wikipedia.org/wiki/Static_build>`_ is a compiled version of a program which has been statically linked against libraries.
A static binary does not depend on library availability of the computer it's running on, usually you can copy this binary on another computer and it will work.
It is still architecture specific (i.e. CPU) and may be kernel (OS version) dependent, so static binaries may be used for portable applications.
For the build to be successful, you may have to install static version of libraries.
