Use the Browser
===============

The Top Menu
------------

The image below shows the top navigation menu of the browser, the top navigation menu
controls most of the browser functionality. From left to right are the browser logo with
version information, the species and assembly information, genomic region locator, a set of
zoom in/out tools, Tracks munu, Apps menu, Settings munu and Documentaion link.

.. image:: _static/topnav.png

Navigator to genomic regions
----------------------------

Click the genomic region locator from top navigation menu, which will popup a window for you
to type a region:

.. image:: _static/region_jump.png

Jump to a Gene
~~~~~~~~~~~~~~

You can type a gene name/symbol, like ``Hox``, when the input content reaches 3 characters, 
the browser will try to find gene symbols start with what you typed:

.. image:: _static/gene_search1.png

if there are hits,
a dropdown menu will popup with isoforms from where you can click, and the browser will then
navigator you to the isoform you chosen.

.. image:: _static/gene_search2.png

Voice input gene symbol
^^^^^^^^^^^^^^^^^^^^^^^

From this set of buttons, |saygene| , click **Say a Gene** button, your web browser
will ask you for permission to access your microphone devices, choose *Allow*, then the browser will
start to listen when you are saying, you can start say letters one by one, like H, O, X, if you click
the red **stop** button, what you said HOX will be put inside of the gene search box and suggested gene symbols
should also be popup, you can then choose the symbols and isoforms you want.

.. |saygene| image:: _static/say_gene.png

.. note:: This feature is dependent on web browser support, web browser without support for
          speech recognition won't see this UI.

Jump to a specific region
~~~~~~~~~~~~~~~~~~~~~~~~~

Below the gene search box, you can also type in genomic coordinates, formats like
``chr6:52258852-52260880`` or ``chr6 52258852 52260880`` can be accepted (it doesn't matter
how many space you have or you are using tabs or not).

.. image:: _static/coord_search.png

Operations in tracks view container
-----------------------------------

Right above the tracks container, there are bunch of tools for operating the tracks, they are
move, re-order, zoom, undo, redo and history tools.

.. image:: _static/tools.png

Move/Re-order/Zoom tool
~~~~~~~~~~~~~~~~~~~~~~~

|movetool| is the default tools selected by the browser. This tools make the browser in ``moving``
mode, when user drag the mouse, the tracks will move along with the dragging. |reordertool| allow
tracks to be re-ordered, user can drag one drag up and down to change the order of tracks. |zoomtool|
allows use to zoom in a specific region use the mouse, when use drag a region and release the mouse,
the browser will zoom into that specific region dragged.

.. |movetool| image:: _static/move_tool.png
.. |reordertool| image:: _static/reorder_tool.png
.. |zoomtool| image:: _static/zoom_tool.png

Undo/Redo/History tool
~~~~~~~~~~~~~~~~~~~~~~

|historytool| contains ``Undo``, ``Redo`` and ``History`` tools, say if you accidently moved
the region you are focusing, you can click ``Undo`` button to go back, and click ``Redo`` allows
you go forward to the step after you clicked ``Undo``, the ``History`` button gives you recent 10
operations and you can jump to, or clear the whole history.

.. |historytool| image:: _static/history_tool.png

.. image:: _static/view_history.png

Settings
--------

``Settings`` menu controls global setting for the browser.

Toggle display of genome Navigator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

By using genome navigator (shown bleow) users can jump to any genomic region,
or whole chromosome(s). 

.. image:: _static/genome_navigator.png

The operations on genome navigator are:

* Left mouse drag: select
* Right mouse drag: pan
* Mousewheel: zoom

The genome navigator can also be hidden to save more space
for the tracks container. Click ``Settings`` on top menu you fill find the switch:

.. image:: _static/show_genome_nav.png


Toggle highlighting of enter region
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When user jump to a region either by gene search or input a genomic coordinate, the entered
region is highlighted by a light yellow box, indicating the user entered region:

.. image:: _static/highlight.png

the highlight can be truned off/on from the switch on ``Settings`` menu:

.. image:: _static/show_highlight.png

Change track lable width
~~~~~~~~~~~~~~~~~~~~~~~~

The default width of track lebels shown below is 120 pixels.

.. image:: _static/label_width.png

The width of track label can be configured by the submenu under ``Settings`` menu:

.. image:: _static/change_label_width.png

Toggle display of VR mode
~~~~~~~~~~~~~~~~~~~~~~~~~

From the ``Settings`` menu use can choose to toggle the VR display mode
of tracks:

.. image:: _static/show_vr.png

Session
-------

Choose ``Session`` from the ``Apps`` menu will bring you the session interface
shown as below:

.. image:: _static/session.png

Save session
~~~~~~~~~~~~

Clike the **Save session** button to save a session, you will also see a session
bundle Id which you can use later to retrieve session. you can save as
many session as you want.

.. image:: _static/save_session.png

Retrieve session
~~~~~~~~~~~~~~~~

the **session bundle Id** can be used later to retrieve a session, paste you session
bundle id in the session interface and click the ``Retrieve session`` button, you would
see the saved sessions before:

.. image:: _static/retrieve_session.png

you will need to choose which session you want to restore:

.. image:: _static/restore_session.png

Click the green *Restore* button, your session will be restored:

.. image:: _static/session_restored.png

Live browsing
-------------

From ``Apps`` menu choose **Go Live**, the browser will navigate you to a new
link, which you can share with someone else, like your collaborator, your PI
or your friends, whatever you operates in you end, people who opened same link
would see same browser view as you.

.. image:: _static/live.png

Screenshot
----------

Users can create publication quality image using *Screenshot* from ``Apps`` menu.
Click the *Screenshot* submenu, a new window will popup and re-rendering all your
tracks as a new SVG file, then you can click the green download button to save
current browser view as a SVG image file.

.. image:: _static/screenshot.png

Track management
----------------

The browser collects data from large corsortiums like Roadmap Epigenomics, ENCODE,
4DN, TaRGER etc. The data are called public data/tracks, and are organized to different
collections, called hubs. Besides these public hubs and tracks, users can also submit
their own tracks and data hub, these are so called custom tracks and hubs.

Add tracks from public hubs
~~~~~~~~~~~~~~~~~~~~~~~~~~~

From ``Tracks`` menu, choose **Public Data Hubs**, for example, for mouse you can see the 
*4D Nucleome Network* hub, click the *Add* button to load this hub:

.. image:: _static/mm10_4dn.png

After the hub was added, a facet table contain all the tracks will popup for you to choose
any tracks you interested:

.. image:: _static/mm10_4dn_facet.png

You can expand the row and/or cloumn selection, to swap row and column:

.. image:: _static/mm10_4dn_facet2.png

Click each cell in the facet table will bring you a new window has table contains all
the tracks in the row and column selection:

.. image:: _static/mm10_4dn_track.png

Click the *Add* button to add the track(s) you want, and you can see the track is added
to the browser view window:

.. image:: _static/mm10_4dn_track_added.png

Add custom tracks or data hub
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Users can also submit their own track as custom track, say we have a bigWig track located at
https://wangftp.wustl.edu/~dli/test/TW463_20-5-bonemarrow_MeDIP.bigWig, from ``Tracks``, choose
**Custom tracks**, will popup the custom track interface, fill in the track type, label and URL,
Click the green *Submit* button:

.. image:: _static/custom_track.png

You can see the track is added:

.. image:: _static/custom_track_added.png

Adding custom data hub is similar, say you have a hub located at https://wangftp.wustl.edu/~dli/test/a.json,
From ``Tracks``, choose **Custom tracks**, choose *Add custom data hub* tab, paste the URL and load the hub
from URL.

.. image:: _static/custom_hub.png

The tracks can then be added from the generated facet table.

.. note:: The tracks from custom hubs are hidden by default as users may submit a hub contains hubdreds
          of tracks. But users can always add the tracks they want from the facet table.

Also see :doc:`tracks` and :doc:`datahub` section for how to prepare your tracks and datahub file.
