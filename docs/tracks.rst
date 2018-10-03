Tracks
======

.. important:: Since all tracks are hosted on the web with HTTP/HTTPS links provided
               for submission as tracks, the webservers which are hosting the track
               files need Cross-Origin Resource Sharing (CORS) enabled.


Quoted from MDN_::

    Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional 
    HTTP headers to tell a browser to let a web application running at 
    one origin (domain) have permission to access selected resources 
    from a server at a different origin. A web application makes a 
    cross-origin HTTP request when it requests a resource that has 
    a different origin (domain, protocol, and port) than its own origin.

.. _MDN: https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS

Configure your webserver to enable CORS
---------------------------------------

Most likely the browser domain is different from the server the tracks are hosted on. The hosting server
needs CORS enabled and for an Apache web server in Ubuntu this setup will work::

    Header always set Access-Control-Allow-Origin "*"
    Header always set Access-Control-Allow-Methods "POST, GET, OPTIONS, DELETE, PUT"
    Header always set Access-Control-Max-Age "1000"
    Header always set Access-Control-Allow-Headers "x-requested-with, Content-Type, origin, authorization, accept, client-security-token"


Prepare track files
-------------------

The browser accesses track files from their URL. Only a portion of the data, that within
the specific view region, are transferred to the browser for visualization. Thus, all
the track files need be hosted in a web accssible location using HTTP or HTTPS. 
The following sections introduce the track types that the browser supports.

Binary track file formats like bigWig_ and HiC_ can be used directly with the browser.
bedGraph_, methylC_, and categorical_ track files need to
be `compressed by bgzip and indexed by tabix`_ for use by the browser.
The resulting index file with suffix ``.tbi`` need be located
at the same URL with the ``.gz`` file.

Bed like format track files need be sorted before submission. For example, if we have a track file named ``track.bedgraph``
we can use the generic Linux ``sort`` command, the ``bedSort`` tool from UCSC, or the ``sort-bed`` command from BEDOPS. Here is an example command using each of the three methods::

    # Using Linux sort
    sort -k1,1 -k2,2n track.bedgraph > track.bedgraph.sorted 
    # Using bedSort
    bedSort track.bedgraph track.bedgraph.sorted
    # Using sort-bed
    sort-bed track.bedgraph > track.bedgraph.sorted

Then the file must be compressed using bgzip and indexed using tabix::

    bgzip track.bedgraph.sorted
    tabix -p bed track.bedgraph.sorted.gz

Move files "track.bedgraph.sorted.gz" and "track.bedgraph.sorted.gz.tbi" to a web server. 
The two files must be in the same directory. Obtain the URL to "track.bedgraph.sorted.gz" for submission.

.. _`compressed by bgzip and indexed by tabix`: http://www.htslib.org/doc/tabix.html

Numerical Tracks
----------------

Currently there are two types of numerical tracks:

* bigWig_
* bedGraph_

bigWig
~~~~~~

``bigWig`` is a popular format to represent numerical values over genomic coordinates.
Please check the `UCSC bigWig`_ page to learn more about this format.

.. _UCSC bigWig: https://genome.ucsc.edu/goldenpath/help/bigWig.html

bedGraph
~~~~~~~~

``bedGraph`` format also defines values in diffenent genomic locations.
For more about the bedGraph format please check `UCSC bedGraph`_ page.

Example lines are below::

    chr12   6537598 6537599 28.80914
    chr12   6537599 6537600 28.96908
    chr12   6537599 6537612 -2
    chr12   6537600 6537601 29.30229

Every line consists of 4 fields separated by the ``Tab`` delimiter. The fields from
left to right are ``chromosome``, ``start position`` (0-based), ``end position`` (not included), and ``value``.

.. note:: You can use negative values for reverse strand. Both positive and negative
          values can exist over the same coordinates (they can overlap). In ``bigWig`` format
          negative values can also be specified, but they cannot overlap with positive values.

.. _UCSC bedGraph: https://genome.ucsc.edu/goldenpath/help/bedgraph.html

Methylation tracks
------------------

Methylation experiments like MeDIP-seq or MRE-seq can use `bigWig`_ or `bedGraph`_ format for data display.
For WGBS if users want to show read depth, methylation context, and methylation
level then the data is best suited for the `methylC`_ format, described below.

methylC
~~~~~~~

Methylation data are formatted in ``methylC`` format, which is a 7 column bed format file::

    chr1    10542   10543   CG      0.923   -       26
    chr1    10556   10557   CHH     0.040   -       25
    chr1    10562   10563   CG      0.941   +       17
    chr1    10563   10564   CG      0.958   -       24
    chr1    10564   10565   CHG     0.056   +       18
    chr1    10566   10567   CHG     0.045   -       22
    chr1    10570   10571   CG      0.870   +       23
    chr1    10571   10572   CG      0.913   -       23

Each line contains 7 fields separated by Tab. The fields are 
``chromosome``, ``start position`` (0-based), ``end position`` (not included),
``methylation context`` (CG, CHG, CHG etc.), ``methylation value``, ``strand``,
and ``read depth``.

Categorical tracks
------------------

Categorical tracks represent genomic bins for different categories. The most popular
example is the represnetation of chromHMM data which indicates which region is likely an enhancer, likely a promoter, etc. 
Other uses for the track include the display of different types of methylation (DMRs, DMVs, LMRs, UMRs, etc.) or even peaks colored by tissue type.

categorical
~~~~~~~~~~~
The ``categorical`` track uses the first three columns of the standard `bed`_ format (``chromosome``, ``start position`` (0-based), and ``end position`` (not included)) with the addition of a 4th column indicating the category type which can be a string or number::

    chr1    start1  end1    category1
    chr2    start2  end2    category2
    chr3    start3  end3    category3
    chr4    start4  end4    category4

Long range chromatin interaction
--------------------------------

Long range chromatin interaction data are used to show relationships between
genomic regions. `HiC`_ is used to show the results from a HiC experiment.

HiC
~~~

Learn more about HiC format please check https://github.com/aidenlab/juicer/wiki/Data.
