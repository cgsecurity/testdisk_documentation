Cross Compilation environment
*****************************
Using Linux, it's possible to generate binaries for Windows.
Two cross-compiler toolchains are available under Fedora to create binaries for Windows 32 and 64 bits.
All packages needed are available at

 * Windows Cygwin target

   * https://copr.fedorainfracloud.org/coprs/grenier/cygwin-testdisk/
   * https://copr.fedorainfracloud.org/coprs/yselkowitz/cygwin/

 * Windows MinGW target

   * https://copr.fedorainfracloud.org/coprs/grenier/mingw-testdisk/

:command:`testdisk`, :command:`photorec` and :command:`fidentify` official binaries are generated using Cygwin,
:command:`qphotorec` using MinGW.
