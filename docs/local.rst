Local track files
=================

We realized that not every group can setup a web server with CORS enabled, since version 48.0.0,
we added the ability to read local track files, which means you can *upload* your track files on
your hard drive to the browser. The formats for the track files are the same as the ones used for
being hosted on webserver.

.. note:: the track *uploaded* through the file upload dialog *cannot* be saved to browser's local
          storage, thus, when you refresh the browser, your local tracks will gone. You need to
          re-upload them (likely re-grant the permission to the browser to read your local files).
          This is a security setup of Javascript. This also means you cannot use your local files
          for datahub.

To use your local track files, format your files to the correct format, open the ``Upload Track``
menu from ``Tracks``:

.. image:: _static/upload1.png

First, choose your track file format:

.. image:: _static/upload2.png

Second, choose your files, you can choose many files of same type if your track only contains one
file, like ``bigWig``, ``bigBed``, ``HiC``, ``bigInteract``, or you can only choose 2 (a pair of) files
if your track need an **index** file, like ``bedGraph``, ``methylC`` etc.

.. image:: _static/upload3.png

Example of choose 2 local bigWig files:

.. image:: _static/upload4.png

The 2 bigWig tracks are added:

.. image:: _static/upload5.png

Example if choose 1 local bedGraph track, (please choose both track file and index file):

.. image:: _static/upload6.png

The bedGraph track is added:

.. image:: _static/upload7.png
