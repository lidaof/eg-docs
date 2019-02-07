Local track files
=================

We realize that not every research group has the ability to set up a web server with CORS enabled. As of version 48.0.0,
we added the ability to read local track files or an entire folder as a datahub. This means the user can *upload* track files
from their hard drive to the browser. The format for these track files is the same as those that are hosted on a webserver.

.. note:: The tracks *uploaded* through the file upload feature *cannot* be saved to the browser's local
          storage. Thus, when you refresh the browser your local tracks will be gone. Tracks need to be
          re-upload to re-grant the browser permission to read  local files.
          This is a security setup of Javascript. To avoid uploading multiple files repeatedly, the user can create
          a ``hub.config.json`` file to specify files as a local datahub. In this manner, after a refresh event the user
          can just upload their local datahub again instead of uploading individual tracks separately.

.. important:: Since the user needs to give permission for the web browser to access
               files on a local hard drive, tracks from a local hard drive **cannot** be saved
               into ``Session``. Please consider using HTTP(S) hosted tracks to work with the session function.

Upload files as tracks
----------------------

To use your local files, make sure to format your files correctly. First, open the ``Upload Track``
menu from ``Tracks``:

.. image:: _static/upload1.png

By default, you will be on the ``Add Local Track`` tab. Second, choose your track file format:

.. image:: _static/upload2.png

Third, choose your files. You can choose many files of same type if the track upload type only requires one
file (``bigWig``, ``bigBed``, ``HiC``, and ``bigInteract``) or if the track upload type requires a data
file and **index** file (``bedGraph``, ``methylC``, etc.) then you need to upload each pair individually.

.. image:: _static/upload3.png

Example upload of 2 local bigWig files:

.. image:: _static/upload4.png

The 2 bigWig tracks are added to the browser view:

.. image:: _static/upload5.png

Example upload of 1 local Bedgraph track and its associated index file:

.. image:: _static/upload6.png

The bedGraph track is added to the browser view:

.. image:: _static/upload7.png

Upload files or a folder as a datahub
-------------------------------------

If you want to upload many different types of track files to the browser, you can do that too!
Choose the ``Add Local Hub`` tab from the track upload menu as before:

.. image:: _static/upload8.png

Create a file called ``hub.config.json`` for the browser to configure your local data hub (example below)::

    [
        {
            "filename": "2value.bg.gz",
            "type": "bedgraph",
            "name": "test bedgraph",
            "options": {"height": 100}
        },
        {
            "filename": "TW463_20-5-bonemarrow_MeDIP.bigWig",
            "type": "bigwig",
            "name": "MeDIP",
            "options": {"color": "pink"}
        },
        {
            "filename": "TW551_20-5-bonemarrow_MRE.CpG.bigWig",
            "type": "bigwig",
            "name": "MRE",
            "options": {"color": "red"}
        },
        {
            "filename": "h1.liftedtohg19.gz",
            "type": "methylc"
        }
    ]

.. note:: Please note the ``name`` and ``options`` attribute specified in this file. The syntax is the same as a remote datahub file.

.. note:: Track files not specified in ``hub.config.json`` will be skipped.

You can either choose an entire folder by clicking the first button:

.. image:: _static/upload9.png

or choose many files by clicking the second button:

.. image:: _static/upload10.png

After uploading either a folder or many files, your local datahub will be displayed: (Please note the ``name``
and ``options`` specified in your ``hub.config.json`` file will also be applied)

.. image:: _static/upload11.png
