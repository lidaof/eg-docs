Datahub
=======

A datahub is a JSON_ file descibing a set of tracks in the browser. A datahub file is an array of tracks,
which are also defined in JSON syntax:

.. code-block:: json

    [
        {
        "type": "track_type1",
        "name": "track_name1",
        "url": "track_url1",
        "options": {
            "color": "red",
            "other option": "other value"
            }
        },
        {
        "type": "track_type2",
        "name": "track_name2",
        "url": "track_url2",
        "options": {
            "color": "red",
            "other option": "other value"
            }
        }
    ]

.. _JSON: http://json.org/


Example bigWig track
--------------------

.. code-block:: json

    {
        "type": "bigwig",
        "name": "example bigwig",
        "url": "https://vizhub.wustl.edu/hubSample/hg19/GSM429321.bigWig",
        "options": {
            "color": "blue",
        }
    }

Supported options: color_, color2_, yScale_, yMax_, yMin_

options
-------

color
~~~~~

color2
~~~~~~

yScale
~~~~~~

yMax
~~~~

yMin
~~~~
