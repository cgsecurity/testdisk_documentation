After using PhotoRec
====================
Usually PhotoRec and QPhotoRec recover a lot of files but without the original filenames, it may be hard to locate the files you are interested in.

Sorting the files by extension
******************************

Using a powershell script under Windows
---------------------------------------
https://github.com/lconte/Copy-PhotoRecFilesbyExtension.ps1

Using a Python script
---------------------
Python comes preinstalled on macOS and most Linux distributions. It can also be installed under Windows.
The Python program `sort-PhotorecRecoveredFiles <https://github.com/tfrdidi/sort-PhotorecRecoveredFiles>`_

 * sorts all files by file extensions into own folders.
 * limits the number of files/folder by creating subfolders if a certain numbers is exceeded. The file/folder number can be customized.
 * For all '''jpgs''': it put them into their own folders per year (EXIF-Data). Within a year, folders for every event are created, e.g. all photos taken at one weekend or vacation are sorted into one folder.

Renaming files using exiftool
*****************************
exiftool can use meta-data from several popular file formats to rename files.
All Linux distributions comes with a package for :command:`exiftool` (file:`perl-Image-ExifTool` for Red Hat, CentOS and Fedora) but otherwise it is available for Windows, Linux and macOS from https://www.sno.phy.queensu.ca/~phil/exiftool/


.. code-block:: none

   exiftool -r -ext avi '-FileName<DateTimeOriginal' -d avi/%Y%m%d_%H%M%S%%-c.%%e avi/
   exiftool -r -ext doc '-FileName<CreateDate' -d doc/%Y%m/%%f.%%e doc/
   exiftool -r -ext jpg '-FileName<DateTimeOriginal' -d sorted_jpg/%Y%m%d/%Y%m%d_%H%M%S%%-c.%%e jpg/
   exiftool -r -ext mov '-FileName<CreateDate' -d mov/%Y%m%d_%H%M%S%%-c.%%e mov/
   exiftool -r -ext mp3 '-FileName<mp3/${artist;} - ${Album;} - ${Track;} - ${Title;}%-c.%e' mp3/f*.mp3
   exiftool -r -ext mp3 '-FileName<mp3/${artist;} - ${Album;} - ${Title;}%-c.%e' -if 'not defined $Track and defined $Title and $Title ne ""' mp3/f*.mp3
   exiftool -r -ext mp3 '-FileName<mp3/${artist;} - ${Title;}%-c.%e' -if 'not defined $Track and not defined $Album and defined $Title and $Title ne ""' mp3/f*.mp3
   exiftool -r -ext mp3 '-FileName<mp3/${artist;} - ${Album;}%-c.%e' -if 'not defined $Track and (not defined $Title or $Title eq "")' mp3/f*.mp3
   exiftool -r -ext ogg '-FileName<ogg/${artist;} - ${Album;} - ${Track;} - ${Title;}%-c.%e' ogg/f*.ogg
   exiftool -r -ext ogg '-FileName<ogg/${artist;} - ${Album;} - ${Title;}%-c.%e' -if 'not defined $Track and defined $Title and $Title ne ""' ogg/f*.ogg
   exiftool -r -ext ogg '-FileName<ogg/${artist;} - ${Title;}%-c.%e' -if 'not defined $Track and not defined $Album and defined $Title and $Title ne ""' ogg/f*.ogg
   exiftool -r -ext ogg '-FileName<ogg/${artist;} - ${Album;}%-c.%e' -if 'not defined $Track and (not defined $Title or $Title eq "")' ogg/f*.ogg
   exiftool -r -ext m4p '-FileName<m4p/${Artist;} - ${Album;} - ${Title;}%-c.%e' m4p/
   exiftool -r -ext mkv '-FileName<%f_${Title;}%-c.%e' mkv/
   exiftool -r -ext mp4 '-FileName<CreateDate' -d mp4/%Y%m%d_%H%M%S%%-c.%%e mp4/
   exiftool -r -ext ps  '-FileName<%f_${Title;}%-c.%e' ps/
   exiftool -r -ext rtf '-FileName<%f_${Title;}%-c.%e' rtf/
   exiftool -r -ext tif '-FileName<DateTimeOriginal' -d sorted_tif/%Y%m%d/%Y%m%d_%H%M%S%%-c.%%e tif/
   exiftool -r -ext ttf '-FileName<ttf/${FontName;}%-c.%e' ttf/
   exiftool -r -ext wma '-FileName<wma/${AlbumArtist;} - ${AlbumTitle;} - ${TrackNumber;}%-c.%e' wma/

   exiftool -r -ext jpg '-FileName<IMG_${FileIndex}%-c.%e' recup_dir.*

Removing duplicated files
*************************
Under Linux, :command:`fslint` can be used to remove duplicated files

.. code-block:: none

   /usr/share/fslint/fslint/findup -d jpg/

