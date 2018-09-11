Tracks
======

This following sections introduce the track types the browser supports.

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
left to right are ``chromosome``, ``start position``, ``end position`` (not included), and ``value``.

.. note:: You can use nagative values for reverse strand, both positive and negative
          values can exist in same coordinates (they can overlap), in ``bigWig`` format
          you can also specify negative values, but they cannot overlap with positive values.

.. _UCSC bedGraph: https://genome.ucsc.edu/goldenpath/help/bedgraph.html

