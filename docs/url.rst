URL parameters
==============

genome
-------

Specify the genome in URL. It's required for all other URL parameters.

Example: ``?genome=hg19``

.. _hub:

hub
---

Specify a data hub URL in JSON format.

Example: ``?genome=hg19&hub=https://vizhub.wustl.edu/public/tmp/a.json``

bundle
-------

Specify a session bundle ID in URL.

Example: ``?genome=hg19&bundle=session-bundle-id``

.. _sessionFile:

sessionFile
-----------

Specify a session file in URL.

Example: ``?sessionFile=https://wangftp.wustl.edu/~dli/test/eg-session--1692c5f0-c392-11e9-829c-912864922e1e.json``

.. note:: ``sessionFile`` can be downloaded using the ``Download current session`` button in Session user interface.
          
          .. image:: _static/sessionFile.png

hicUrl
------

Specify an HiC track in URL.

Example: ``?genome=hg19&hicUrl=https://your.url.to.hic.file``

position
--------

Specify the default genomic position once the browser is loaded.

Example: ``?genome=hg19&position=chr1:1000-2000``

noDefaultTracks
---------------

Remove the default tracks when load a data hub.

Example: ``?genome=hg19&noDefaultTracks=1``

datahub
-------

Redirects to the legacy browser.

Example: ``?genome=hg19&datahub=https://your.url.to.datahub``

session
--------

Redirects to the legacy browser.

Example: ``?genome=hg19&session=legacy-browser-session-id``
