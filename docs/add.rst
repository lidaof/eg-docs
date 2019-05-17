Add a new genome
================

Here we will use mouse ``mm10`` for example to illustate how to add a new genome build to the Browser.

Prepare genome sequence file
----------------------------

The browser expect genome sequence file in the 2bit_ file developed by UCSC, for mouse mm10,
you can get it from http://hgdownload.soe.ucsc.edu/goldenPath/mm10/bigZips/mm10.2bit,
after download the 2bit file, you will need put the 2bit file on a web place with CORS access.

.. _2bit: http://genome.ucsc.edu/FAQ/FAQformat.html#format7

Create the folder for genome configuration files
------------------------------------------------

Create a folder called ``mm10`` under ``frontend/src/model/genomes``, now all the files
listed below should be placed under this new mm10 folder.

Get cytoband file
~~~~~~~~~~~~~~~~~

Download the cytoband information from http://hgdownload.soe.ucsc.edu/goldenPath/mm10/database/cytoBandIdeo.txt.gz, unzip
it, run the following command to get a file called cytoBand.json::

    node frontend/src/model/genomes/cytobandTextToJson.js cytoBandIdeo.txt

Prepare annotation annotation tracks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the mm10 folder, create a file called ``annotationTracks.json`` with following content::

    {
        "Ruler": [
            {
                "type": "ruler",
                "label": "Ruler",
                "name": "Ruler"
            }
        ],
        "Genes": [
            {
                "name": "refGene",
                "label": "RefSeq genes",
                "filetype": "geneAnnotation"
            },
            {
                "name": "gencodeM19",
                "label": "GENCODE M19 genes",
                "options": {
                    "categoryColors": {
                        "coding": "rgb(0,60,179)",
                        "nonCoding": "rgb(0,128,0)",
                        "pseudogene": "rgb(230,0,172)",
                        "problem": "rgb(255,0,0)",
                        "polyA": "rgb(0,0,51)"
                    }
                },
                "filetype": "geneAnnotation"
            },
            {
                "name": "gencodeM19Basic",
                "label": "GENCODE M19 genes (basic set)",
                "options": {
                    "categoryColors": {
                        "coding": "rgb(0,60,179)",
                        "nonCoding": "rgb(0,128,0)",
                        "pseudogene": "rgb(230,0,172)",
                        "problem": "rgb(255,0,0)",
                        "polyA": "rgb(0,0,51)"
                    }
                },
                "filetype": "geneAnnotation"
            }
        ],
        "RepeatMasker": {
            "All Repeats": [
                {
                    "name": "rmsk_all",
                    "label": "RepeatMasker",
                    "filetype": "repeatmasker",
                    "url": "https://vizhub.wustl.edu/public/mm10/rmsk16.bb",
                    "height": 30
                }
            ]
        },
        "Genome Comparison": [
            {
                "name": "hg38tomm10",
                "label": "Human hg38 to mm10 blastz",
                "querygenome": "hg38",
                "filetype": "genomealign",
                "url": "https://vizhub.wustl.edu/public/mm10/weaver/mm10_hg38_axt.gz"
            }
        ]
    }

Get chromosome sizes
~~~~~~~~~~~~~~~~~~~~

Download the file from http://hgdownload.soe.ucsc.edu/goldenPath/mm10/bigZips/mm10.chrom.sizes,
you can following awk command to create the ``chromSize.json`` file::

    sort -V myoLuc2.chrom.sizes | awk 'BEGIN{print "["}{ print "\t{\"chr\": \""$1"\", \"size\": "$2"},"}END{print "]"}' > chromSize.json

Move the ``chromSize.json`` file into the mm10 folder.

Create genome configuration file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create a file called ``mm10.js``, filling the following contents::

    import Chromosome from '../Chromosome';
    import Genome from '../Genome';
    import TrackModel from '../../TrackModel';
    import cytobands from './cytoBand.json';
    import annotationTracks from "./annotationTracks.json";
    import chromSize from "./chromSize.json";
    
    const allSize = chromSize.map(genom => new Chromosome(genom.chr, genom.size));
    const genome = new Genome("myoLuc2", allSize);

    const navContext = genome.makeNavContext();
    const defaultRegion = navContext.parse("chr6:52425276-52425961");
    const defaultTracks = [
        new TrackModel({
            type: "geneAnnotation",
            name: "refGene",
            genome: "mm10",
        }),
        new TrackModel({
            type: "geneAnnotation",
            name: "gencodeM19Basic",
            genome: "mm10",
        }),
        new TrackModel({
            type: "ruler",
            name: "Ruler",
        }),
        new TrackModel({
            type: 'repeatmasker',
            name: 'RepeatMasker',
            url: 'https://vizhub.wustl.edu/public/mm10/rmsk16.bb',
        })
    ];

    const publicHubData = {
        "4D Nucleome Network": "The 4D Nucleome Network aims to understand the principles underlying nuclear " + 
        "organization in space and time, the role nuclear organization plays in gene expression and cellular function, " +
        "and how changes in nuclear organization affect normal development as well as various diseases.  The program is " +
        "developing novel tools to explore the dynamic nuclear architecture and its role in gene expression programs, " + 
        "models to examine the relationship between nuclear organization and function, and reference maps of nuclear" + 
        "architecture in a variety of cells and tissues as a community resource.",
        "Encyclopedia of DNA Elements (ENCODE)": "The Encyclopedia of DNA Elements (ENCODE) Consortium is an " +
            "international collaboration of research groups funded by the National Human Genome Research Institute " +
            "(NHGRI). The goal of ENCODE is to build a comprehensive parts list of functional elements in the human " +
            "genome, including elements that act at the protein and RNA levels, and regulatory elements that control " +
            "cells and circumstances in which a gene is active.",
    };

    const publicHubList = [
        {
            collection: "4D Nucleome Network",
            name: "4DN HiC datasets",
            numTracks: 23,
            oldHubFormat: false,
            url: "https://vizhub.wustl.edu/public/mm10/4dn_mm10.json",
            description: {
                'hub built by': 'Daofeng Li (dli23@wustl.edu)',
                'hub built date': 'Sep 1 2018',
                'hub built notes': 'metadata information are obtained directly from 4DN data portal'
            },
        }
    ]

    const MM10 = {
        genome: genome,
        navContext: navContext,
        cytobands: cytobands,
        defaultRegion: defaultRegion,
        defaultTracks: defaultTracks,
        twoBitURL: "https://vizhub.wustl.edu/public/mm10/mm10.2bit",
        publicHubData,
        publicHubList,
        annotationTracks,
    };

    export default MM10;

defaultRegion
^^^^^^^^^^^^^

This variable controls the default region when you open the browser for mm10.

defaultTracks
^^^^^^^^^^^^^

This variable controls default tracks when you open the browser for mm10.

publicHubList
^^^^^^^^^^^^^

The field contains a list of public hubs.

Add the new genome to the system
--------------------------------

Modify ``frontend/src/model/genomes/allGenomes.ts``::

    import MM10 from './mm10/mm10';

Include ``MM10`` to ``allGenomes`` variable::

    const allGenomes = [
        HG19,
        HG38,
        MM10,
        PANTRO5,
        DAN_RER10,
        RN6,
    ];

In variable ``treeOfLife`` add the entry for mm10::

    mouse: {
        logoUrl: 'https://epigenomegateway.wustl.edu/browser/images/Mouse.png',
        assemblies: [ MM10.genome.getName() ],
        color: 'white',
    },

.. note:: one species can have many assemblies, you can also include *mm9* in the ``assemblies`` array.

Save all the edits, restart the browser (or recompile) you can see the new added genome assembly.
