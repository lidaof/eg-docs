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
            "color": "red",
            "backgroundColor":"#FFE7AB"
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
            "color": "blue",
            "backgroundColor":"#C0E3CC"
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
    
Example methylC track
--------------------

.. code-block:: json

  {
    "type": "methylc",
    "name": "H1",
    "url": "https://vizhub.wustl.edu/public/hg19/methylc2/h1.liftedtohg19.gz",
    "isSelected": false,
    "options": {
      "label": "Methylation",
      "colorsForContext": {
        "CG": { "color": "#648bd8", "background": "#d9d9d9" },
        "CHG": { "color": "#ff944d", "background": "#ffe0cc" },
        "CHH": { "color": "#ff00ff", "background": "#ffe5ff" }
      },
      "depthColor": "#01E9FE"
    },
  }

Example categorical track
--------------------

.. code-block:: json

  {
    "type": "methylc",
    "name": "ChromHMM",
    "url": "https://egg.wustl.edu/d/hg19/E017_15_coreMarks_dense.gz",
    "isSelected": false,
    "options": {
      "label": "ChromHMM107",
      "colorsForContext": {
        "1": { "color": "#FF0000"},
        "2": { "color": "#FF4500"},
        "3": { "color": "#32Cd32"}
      }
    }
  }


Supported options: backgroundColor_, color_, color2_, yScale_, yMax_, and yMin_

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

*Requried*. ``name`` specifies the track name used internally by the browser. It is also 
displayed as the track legend if no label_ speficied. Value can be any string.

label
~~~~~

*Optional*. ``label`` specifies the track legend displayed in the browser. It overrides the name_ arrtibute.
Value can be any string.

url
~~~

*Requried*. ``url`` contains the URL to the track file and needs to be HTTP or HTTPS location string.

.. important:: A ``url`` is requried for all the tracks in binary format. Gene annotaion tracks,
               like ``refGene``, do not need a ``url`` as they are stored in the Mongo database. 
               Additional annotation tracks, such as the ``ruler`` track, also do not need a ``url``.
               
.. caution:: Each user-provided ``url`` must link to a publically available website, without password 
             protection, so that the browser can read in the file. 

metadata
~~~~~~~~

*Optional*. An object specifying the metadata of the track. 

In this basic example the value of each metadata term is a **string**. ::

    "metadata": {
        "sample": "bone",
        "assay": "MRE"
    }

This example public Roadmap data hub has more complex metadata definitions and makes use of a **list of strings** 
to build a *hierarchical structure*. ::

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

The list of metadata is ordered from more generic to more specific and 
 helps build the facet table hierarchy making the **search** and **filter** functions in track table easier.

details
~~~~~~~

*Optional*. If you want to add more information for each track then the ``details`` attribute is helpful.
After right clicking on the track you can click **More Information** and see the 
``details``, ``url``, and ``metadata`` for each track in the dropdown menu. ::

    "details": {
        "data source": "Roadmap Project",
        "date collected": "May 7 2016"
    }

options
~~~~~~~

*Optional*. All track render options are placed in an object called ``options``.
This object can have the following properties:

color
^^^^^

``color`` is used to define the color for each track. A color name, RGB values, or hex color code can be used.
For more about color name or RGB please see https://www.w3schools.com/css/css_colors.asp.

color2
^^^^^^

``color2`` is used to define the color for negative values from the track data. The default is
the same as color_.

backgroundColor
^^^^^^^^^^^^^^^

``backgroundColor`` defines the background color of the track.

height
^^^^^^

``height`` controls the height of the track which is specified as a number and displayed in *pixels*.

yScale
^^^^^^

``yScale`` allows you to configure the track's y-scale. Options include *auto* or *fixed*.
*auto* sets the y-scale from 0 to the max value of values in the view region for a given track. 
*fixed* means you can specify the *minimal* and *maximal* value.

yMax
^^^^

``yMax`` is used to define the *maximum* value of a track's y-axis. Value is number.

yMin
^^^^

``yMin`` is used to define the *minimum* value of a track's y-axis. Value is number.

.. important:: If you need the track to be in *fixed* scale, you need to specify ``yScale`` to *fixed*
               besides of set ``yMax`` and ``yMin``.

colorAboveMax
^^^^^^^^^^^^^

``colorAboveMax`` defines the color displayed when a *fixed* yScale_ is used and a value exceeds the 
yMax_ defined.

color2BelowMin
^^^^^^^^^^^^^^

``color2BelowMin`` defines the color displayed when a *fixed* yScale_ is used and a value is below the
yMin_ defined.

displayMode
^^^^^^^^^^^

``displayMode`` specifies display mode for each tracks. Different tracks have different display modes as listed below.

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
