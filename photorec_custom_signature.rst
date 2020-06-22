Creating custom signature for PhotoRec
======================================

PhotoRec recognizes numerous file formats. More than 480 file extensions (about 300 file families) are referenced.
In example, PhotoRec is able to identify the JPEG file format and it can recover lost files using this format whatever the original file extension (jpg, jpeg, JPG...).

To check if a file format is already recognized, you can

 * consult the `file formats <https://www.cgsecurity.org/wiki/File_Formats_Recovered_By_PhotoRec>`_.
 * submit a sample file to the `PhotoRec online checker <https://www.cgsecurity.org/photorec/>`_.
 * use :command:`fidentify` on a file sample (See :ref:`running_fidentify_win` or :ref:`running_fidentify_linux`)

.. code-block:: none

	[kmaster@adsl ~]$ fidentify /home/kmaster/src/testfiles/sample.pfi
	/home/kmaster/src/testfiles/sample.pfi: unknown


In this case, the file type is listed as **unknown**, so PhotoRec can't recover this kind of file, at least for the moment. We will check if it's possible to add a custom signature for it.

If instead of unknown an extension is listed, PhotoRec knows this file format, it may recover the file with another extension than the extension you are used to.

Signature Syntax
****************

The file must contain one signature definition per line. A signature is composed of

 * extension name
 * offset of the signature
 * signature or magic value

The magic value can be composed of

 * a string, e.g. "data". Special characters can be escaped like "\b", "\n", "\r", "\t", "\0" or "\\".
 * hexadecimal data, e.g. 0x12, 0x1234, 0x123456... Note that `0x123456`, `0x12 0x34 0x56` and `0x12, 0x34, 0x56` are equivalents.
 * space or comma delimiters are ignored

By using an hexadecimal editor, you can see that the :file:`pfi` file from our example begins by a distinctive string `PhotoFiltre Image` at offset 0.

.. code-block:: none

	[kmaster@adsl ~]$ hexdump -C /home/kmaster/src/testfiles/sample.pfi | head
	00000000  50 68 6f 74 6f 46 69 6c  74 72 65 20 49 6d 61 67  |PhotoFiltre Imag|
	00000010  65 03 40 06 00 00 b0 04  00 00 40 19 01 00 40 19  |e.@.......@...@.|
	00000020  01 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|

The signature can be written as

.. code-block:: none

	pfi 0 "PhotoFiltre Image"

or

.. code-block:: none

	pfi 0 "PhotoFiltre", 0x20, "Image"

or if you prefer hexadecimal

.. code-block:: none

	pfi 0 0x50686f746f46696c74726520496d616765

From :command:`fidentify`/:command:`photorec` point of view, the signatures are identical.

.. warning::
   Be careful, :command:`hexdump` displays non-printable chars as dots. The following signature is wrong:

   .. code-block:: none

           pfi 0 "PhotoFiltre Image."

   This signature using an hexadecimal value instead of a dot is correct:

   .. code-block:: none

           pfi 0 "PhotoFiltre Image", 0x03



File location
*************

PhotoRec searches for the signature file named

 * Windows: :file:`photorec.sig` in the `USERPROFILE` or `HOMEPATH` directory, e.g. :file:`C:\\Documents and Settings\\bob\\` or :file:`C:\\Users\\bob`.
 * Linux and macOS: :file:`.photorec.sig` in the `HOME` directory, e.g. :file:`/home/bob`
 * :file:`photorec.sig` in the current directory

This file doesn't exist by default, you need to create one.
Using a text editor (e.g. notepad, vim...), create the signature file and add the signature you have identified.

Check your custom signature with fidentify
******************************************

:command:`fidentify` now perfectly identify the file

.. code-block:: none

	[kmaster@adsl ~]$ fidentify /home/kmaster/src/testfiles/sample.pfi
	/home/kmaster/src/testfiles/sample.pfi: pfi

If :command:`fidentify` doesn't recognize the signature,

 * check your signature, it may be incorrect
 * **verify that the signature file is a true ASCII text file**. It must not begin by `EF BB BF` (UTF-8 Byte Order Mark) or `FF FE` (UTF-16 LE BOM) by example.
 * verify the filename of your signature file

Run PhotoRec
************

You are now ready to use PhotoRec with your custom signature to recover your files.
If a signature file is present, PhotoRec will use it by default.

Improved file recover
**********************

To control all aspects of the recovery (file content check, file size control, footer detection...),
the best way to add a signature, if you are developer, is to `modify PhotoRec <http://www.cgsecurity.org/wiki/Developers#Adding_a_new_file_format_to_PhotoRec>`_ itself.

**Commercial support is also available from the author** grenier@cgsecurity.org.
