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
            "color": "red"
            }
        },
        {
        "type": "track_type2",
        "name": "track_name2",
        "url": "track_url2",
        "options": {
            "color": "blue"
            }
        }
    ]

.. _JSON: http://json.org/

Example data hub
----------------

Pasted below is an example data hub for mouse mm10:

.. code-block:: json

    [
        {
        "type": "bigwig",
        "url": "https://wangftp.wustl.edu/~dli/test/TW463_20-5-bonemarrow_MeDIP.bigWig",
        "name": "MeDIP",
        "options": {
            "color": "red"
            },
        "metadata": {
            "sample": "bone",
            "assay": "MeDIP"
            }
        },
        {
        "type": "bigwig",
        "url": "https://wangftp.wustl.edu/~dli/test/TW551_20-5-bonemarrow_MRE.CpG.bigWig",
        "name": "MRE",
        "options": {
            "color": "blue"
            },
        "metadata": {
            "sample": "bone",
            "assay": "MRE"
            }
        }
    ]


Example bigWig track
--------------------

.. code-block:: json

    {
        "type": "bigwig",
        "name": "example bigwig",
        "url": "https://vizhub.wustl.edu/hubSample/hg19/GSM429321.bigWig",
        "options": {
            "color": "blue"
        }
    }

Supported options: color_, color2_, yScale_, yMax_, yMin_

Track properties
----------------

type
~~~~

*Requried*. ``type`` specifies the track type, currently supported track types:

* bigWig
* bedGraph
* methylC
* categorical
* hic
* bed
* bigbed
* repeatmasker
* geneAnnotation
* genomealign

.. note:: ``type`` is case insensitive.

name
~~~~

*Requried*. ``name`` specifies the track name used internally by the browser. It's aso used for
display as track legend if no label_ speficied. Value can be any string.

label
~~~~~

*Optional*. ``label`` specifies the track legend displayed in the browser. It overrites the name_ arrtibute.
Value can be any string.

url
~~~

*Requried*. ``url`` contains the URL to the track file, need to be HTTP or HTTPS location string.

.. important:: ``url`` is requried for all the tracks in binary format. While for gene annotaion tracks
               like ``refGene``, it's not requried, since the data are stored in Mongo database. Another
               case is ``ruler`` track, ``url`` is also not needed.


metadata
~~~~~~~~

*Optional*. An object speficies the metadata of the track. Examples like::

    "metadata": {
        "sample": "bone",
        "assay": "MRE"
    }

the value of each metadata term can be a **string** or a **list of string** with *hirarchical structure*, for
example, the public Roamap hub have metadata definition like::

    {
        "url": "https://egg.wustl.edu/d/hg19/GSM997242_1.bigWig", 
        "metadata": {
            "Sample": [
                "Adult Cells/Tissues", 
                "Blood", 
                "Other blood cells", 
                "CD4+_CD25-_Th_Primary_Cells"
            ],    
            "Donor": [
                "Donor Identifier", 
                "Donor_332"
            ],    
            "Assay": [
                "Epigenetic Mark", 
                "Histone Mark", 
                "H3", 
                "H3K9", 
                "H3K9me3"
            ],    
            "Institution": [
                "Broad Institute"
            ]     
        },    
        "type": "bigwig", 
        "options": {
            "color": "rgb(159,0,72)"
        },    
        "name": "H3K9me3 of CD4+_CD25-_Th_Primary_Cells"
    }

The list of metadata has order from more generic to more specific, and 
this helps build the facet table hierarchy, make **search** and **filter** in track table easier.

details
~~~~~~~

*Optional*. If you want to more information to be shown on right click the track, you can put
them in ``details`` attribute, contents put here will be displayed when right click the track,
and toggle the **More Information** dropdown menu::

    "details": {
        "data source": "Roadmap Project",
        "date collected": "May 7 2016"
    }

options
~~~~~~~

*Optional*. All track render options are placed in an object called ``options``.
this object can have the following properties:

color
^^^^^

``color`` is used to define the color for the track, color name, RGB values can be used.
For more about color name or RGB, please check https://www.w3schools.com/css/css_colors.asp.

color2
^^^^^^

``color2`` is used to define the color for negative values from the track data. Default is
the same as color_.

backgroundColor

``backgroundColor`` defines the background color of the track.

height
^^^^^^

``height`` controls the height of the track, speficied in number, unit is *pixel*.

yScale
^^^^^^

``yScale`` allows you to configure the track's y-scale, you can use *auto* or *fixed*
here. *auto* means the y-scale will be calculated from the values in view region, from 0
to maximal of values in view region. *fixed* means you can specify the *minimal* and *maximal* value.

yMax
^^^^

``yMax`` used to define the *maximal* value of track y-axis. Value is number.

yMin
^^^^

``yMin`` used to define the *minimal* value of track y-axis. Value is number.

.. important:: If you need the track to be in *fixed* scale, you need to specify ``yScale`` to *fixed*
               besides of set ``yMax`` and ``yMin``.

colorAboveMax
^^^^^^^^^^^^^

``colorAboveMax`` defines the color when yScale_ set to *fixed*, and the value exceeds the value
yMax_ defined.

color2BelowMin
^^^^^^^^^^^^^^

``color2BelowMin`` defines the color when yScale_ set to *fixed*, and the value below the value
yMin_ defined.

displayMode
^^^^^^^^^^^

``displayMode`` specifies display mode for tracks, different tracks have different display mode
supported. 


.. list-table::
   :widths: 25 50
   :header-rows: 1

   * - type
     - display mode
   * - bigWig
     - *auto*, *bar*, *heatmap*
   * - bedGraph
     - *auto*, *bar*, *heatmap*
   * - geneAnnotation
     - *full*, *density*
   * - HiC
     - *arc*, *heatmap*
   * - genomealign
     - *rough*, *fine*
