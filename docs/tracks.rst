Tracks
======

This following sections introduce the track types the browser supports.

Prepare track files
-------------------

The browser access the track files from its URL, only the proportion of the data in
the specific viewed region are transferred to the browser for visualization. Thur, all
the track files need be hosted in a web accssible location use HTTP or HTTPS.

Binary track file format like bigWig_ and HiC_ can be used directly with the browser.
bedGraph_, methylC_ and categorical_ track files need 
be `compressed by bgzip and indexed by tabix`_ for used by the browser.
The resulted index file with suffix ``.tbi`` need be located
at the same URL with the ``.gz`` file.

Bed like format track files need be sorted first, say we have a track file named ``track.bedgraph``,
we can use generic Linux ``sort`` command or the ``bedSort`` tool from UCSC. The following 2 commands
do the same thing.

    sort -k1,1 -k2,2n track.bedgraph > track.bedgraph.sorted
or
    bedSort track.bedgraph track.bedgraph.sorted

then compressed and index using tabix:

    bgzip track.bedgraph.sorted
    tabix -p bed track.bedgraph.sorted.gz

Move files "track.bedgraph.sorted.gz" and "track.bedgraph.sorted.gz.tbi" to a web server. 
The two files must be in the same directory. Obtain the URL to "track.bedgraph.sorted.gz" for submission.

.. _`compressed by bgzip and indexed by tabix`: http://www.htslib.org/doc/tabix.html

Configure your webserver to enable CORS
-------------------------------------

Quoted from MDN_:

    Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers
    to tell a browser to let a web application running at one origin (domain) 
    have permission to access selected resources from a server at a different origin. 
    A web application makes a cross-origin HTTP request when it requests a resource that
    has a different origin (domain, protocol, and port) than its own origin.

.. _MDN: https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS

Since the browser domain is different with the server the tracks are hosted, the hosting server
need enable CORS, for Apache web server in Ubuntu, this setup would work:

    Header always set Access-Control-Allow-Origin "*"
    Header always set Access-Control-Allow-Methods "POST, GET, OPTIONS, DELETE, PUT"
    Header always set Access-Control-Max-Age "1000"
    Header always set Access-Control-Allow-Headers "x-requested-with, Content-Type, origin, authorization, accept, client-security-token"


Numerical Tracks
----------------

Currently there are two types of numerical tracks:

* bigWig_
* bedGraph_

bigWig
~~~~~~

``bigWig`` is a popular format to represent numerical values over genomic coordinates.
Please check `UCSC bigWig`_ page to learn more about this format.

.. _UCSC bigWig: https://genome.ucsc.edu/goldenpath/help/bigWig.html


bedGraph
~~~~~~~~

``bedGraph`` format also defines values in diffenent genomic locations.
More about bedGraph please check `UCSC bedGraph`_ page.

Example lines are below::

    chr12   6537598 6537599 28.80914
    chr12   6537599 6537600 28.96908
    chr12   6537599 6537612 -2
    chr12   6537600 6537601 29.30229

Every line consists of 4 fields separated by ``Tab`` delimiter,the fields from
left to right are ``chromosome``, ``start position`` (0-based), ``end position`` (not included), and ``value``.

.. note:: You can use nagative values for reverse strand, both positive and negative
          values can exist in same coordinates (they can overlap), in ``bigWig`` format
          you can also specify negative values, but they cannot overlap with positive values.

.. _UCSC bedGraph: https://genome.ucsc.edu/goldenpath/help/bedgraph.html

Methylation tracks
------------------

methylC
~~~~~~~

Methylation data are formatted in ``methylC`` format, which is a 7 column bed format file.

Categorical tracks
------------------

categorical
~~~~~~~~~~~

Long range chromatin interaction
--------------------------------

HiC
~~~

