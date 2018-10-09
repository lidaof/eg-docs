Use the Browser
===============

The Top Menu
------------
.. image:: _static/topnav.png

The top navigation menu (above) controls most of the browser functionality. From left to right are the browser logo with
version information, species and assembly information, genomic region locator, zoom in/out tools, Tracks menu, Apps menu, Settings menu and Documentaion link.


Genomic Region Locator
----------------------
.. image:: _static/region_jump.png
   :width: 60px

The genomic region locator allows the user to navigate to a region or gene. 

Gene Search
~~~~~~~~~~~

You can type a gene name/symbol, like ``Hox``, and when the input content reaches 3 characters 
the browser will try to find gene symbols starting with what you typed:

.. image:: _static/gene_search1.png
   :width: 60px

After a gene is selected a dropdown menu will pop up with isoforms for the gene. After clicking an isoform the browser will navigate you to its genomic region. 

.. image:: _static/gene_search2.png
   :width: 60px

Voice input gene symbol
^^^^^^^^^^^^^^^^^^^^^^^

From this set of buttons, |saygene| , click the **Say a Gene** button, your web browser
will ask you for permission to access your microphone devices, choose *Allow*, and the browser will
start to listen to what you are saying. You can start saying letters one by one, like H, O, X, if you click
the red **stop** button, what you said "HOX" will populate the gene search box and suggested gene symbols will pop up. As before you can then choose the gene and isoform you want to navigate to.

.. |saygene| image:: _static/say_gene.png

.. note:: This feature is dependent on web browser support. A web browser without support for
          speech recognition won't see this UI.

Region Search 
~~~~~~~~~~~~~

Below the gene search box you can use the region search box to navigate to specific genomic coordinates. Formats such as
``chr6:52258852-52260880`` or ``chr6 52258852 52260880`` are accepted (the browser is not sensitive to the number of spaces or tabs between the `chr`, `start`, and `stop`. 

.. image:: _static/coord_search.png

Operations in the Tracks View Container
---------------------------------------
.. image:: _static/tools.png

Right above the tracks on the left hand side there are a bunch of tools for operating on the tracks. From left to right these include the
move, re-order, zoom, undo, redo, and history tools.


Move/Re-order/Zoom tools
~~~~~~~~~~~~~~~~~~~~~~~~

The |movetool| is the default tool selected by the browser. ``Moving``
mode allows the user to drag the mouse right or left and the tracks will move along mouse moving to new regions. The |reordertool| allows
tracks to be ``re-ordered``. The user can drag one or more tracks up or down to change the order of tracks. The |zoomtool|
allows the user to ``zoom in`` on a specific region within the current view using the mouse.

.. |movetool| image:: _static/move_tool.png
.. |reordertool| image:: _static/reorder_tool.png
.. |zoomtool| image:: _static/zoom_tool.png

Undo/Redo/History tools
~~~~~~~~~~~~~~~~~~~~~~~

|historytool| contains the ``Undo``, ``Redo``, and ``History`` tools. For instance if you accidently moved
to another region and forgot what you were looking at before you can click the ``Undo`` button to go back. Clicking the ``Redo`` button allows you to go forward to the step before you clicked ``Undo``. The ``History`` button gives you the 9 most recent
operations and allows you to jump to any of these operations or clear the history.

.. |historytool| image:: _static/history_tool.png

.. image:: _static/view_history.png

Settings
--------

The ``Settings`` menu controls global settings for the browser.

Toggle display of the Genome Navigator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

By using the genome navigator (below) users can jump to any genomic region
or chromosome(s). 

.. image:: _static/genome_navigator.png

The operations on the genome navigator are:

* Left mouse drag: select
* Right mouse drag: pan
* Mousewheel: zoom

The genome navigator can also be hidden to save space
when viewing tracks. Click ``Settings`` on the top menu and uncheck the box to switch off this feature:

.. image:: _static/show_genome_nav.png

Toggle highlighting of enter region
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When a user jumps to a region or gene using the Genomic Region Locator, that region or gene
is highlighted with a light yellow box.

.. image:: _static/highlight.png

This highlighting can be turned off/on by clicking the botton on the ``Settings`` menu:

.. image:: _static/show_highlight.png

Change track label width
~~~~~~~~~~~~~~~~~~~~~~~~

The default width of track labels (below) is 120 pixels.

.. image:: _static/label_width.png

The width of the track label can be configured by the submenu under the ``Settings`` menu:

.. image:: _static/change_label_width.png

Toggle display of VR mode
~~~~~~~~~~~~~~~~~~~~~~~~~

From the ``Settings`` menu the user can choose to toggle the VR display mode
of tracks:

.. image:: _static/show_vr.png

After choose the **Show 3D scene** submenu, a new container with VR view of the tracks will appear:

.. image:: _static/vr.png

You can click the |vricon| icon at the bottom right to toggle the full screen display of VR mode, then you can
use your mouse and keys ``W``, ``A``, ``S`` and ``D`` to control the view of VR mode, like this view below
can easily show you the interaction between two genomic loci and methylation status along this region.

.. |vricon| image:: _static/vr_icon.png

.. image:: _static/vr2.png

Apps
----

Session
~~~~~~~

Choosing ``Session`` from the ``Apps`` menu will bring you to the session interface
shown below:

.. image:: _static/session.png

Save session
^^^^^^^^^^^^

Click the **Save session** button to save a session. A session
bundle Id will be created which allows the user to retrieve their session at a later date.

.. image:: _static/save_session.png

Retrieve session
^^^^^^^^^^^^^^^^

The **session bundle Id** can be used later to retrieve a session by pasting the session
bundle id in the session interface and clicking the ``Retrieve session`` button.

.. image:: _static/retrieve_session.png

Choose which session status you want to restore:

.. image:: _static/restore_session.png

Click the green *Restore* button and your session will be restored:

.. image:: _static/session_restored.png

Live browsing
~~~~~~~~~~~~~

From the ``Apps`` menu choose **Go Live**, the browser will navigate you to a new
link which you can share with someone else, like your collaborator, your PI,
or your friends. Whatever operations are done by you are mirrored on the displays of the people who opened the same link.

.. image:: _static/live.png

Screenshot
~~~~~~~~~~

Users can create publication quality images using the *Screenshot*  tool from the ``Apps`` menu.
Click the *Screenshot* button and a new window will po pup that re-renders all your
tracks as a new SVG file. Once rendered you can click the green download button to save the
current browser view as a SVG image file.

.. image:: _static/screenshot.png

Track management
----------------

The browser collects data from large corsortia like Roadmap Epigenomics, ENCODE,
4DN, TaRGET, etc. The data are called public data/tracks and are organized into different
collections called hubs. Along with these public hubs and tracks users can submit
their own custom tracks and data hubs to allow for easy comparison.

Add tracks from public hubs
~~~~~~~~~~~~~~~~~~~~~~~~~~~

From the ``Tracks`` menu choose **Public Data Hubs**. This will display all of the public data hubbs available for the species and build you are currently working in. For example, using mouse mm10 annotation the *4D Nucleome Network* hub is available. Click the *Add* button to load this hub:

.. image:: _static/mm10_4dn.png

After a hub is added, a facet table containing all tracks will pop up. This allows you to choose
any tracks you are interested in:

.. image:: _static/mm10_4dn_facet.png

You can expand the row and/or column selection by clicking the ``+`` buttons. Row and column displays can also be easily swapped:

.. image:: _static/mm10_4dn_facet2.png

Clicking a cell within the facet table will pop up a new window containing a table with the tacks that match the row and column selections: 

.. image:: _static/mm10_4dn_track.png

Click the *Add* button to add the track(s) you want. You can then view tracks in the browser view window:

.. image:: _static/mm10_4dn_track_added.png

Adding custom tracks or data hub
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Users can also submit their own track as a custom track. For example, say we have a bigWig track located at
https://wangftp.wustl.edu/~dli/test/TW463_20-5-bonemarrow_MeDIP.bigWig . From the ``Tracks`` menu choose
**Custom tracks** and a custom track interface will pop up. Fill in the track type, label, and URL before clicking
the green *Submit* button:

.. image:: _static/custom_track.png

You can see the track is added:

.. image:: _static/custom_track_added.png

Adding a custom data hub is similar to the steps above. For example, say you have a hub located at https://wangftp.wustl.edu/~dli/test/a.json . From the ``Tracks`` menu choose **Custom tracks**, switch to the *Add custom data hub* tab, paste the URL of your hub, and then click the green *Load From URL* button. 
from URL.

.. image:: _static/custom_hub.png

The tracks within the custom hub can then be added from the generated facet table.

.. note:: Tracks from custom hubs are hidden by default as users may submit a hub contains hundreds 
          of tracks. Users should add tracks that they want from the facet table.

You can also load a local data hub file in JSON format from your computer using the *file upload* interface, right below the *URL submit* hub interface.

Also see the :doc:`tracks` and :doc:`datahub` sections for how to prepare your tracks and datahub files.

Track Customization
-------------------

Tracks can be customized in a multitude of manners. 

Selecting Tracks
~~~~~~~~~~~~~~~~

An indivdual track can be selected by simply right clicking on the tracking on the track. Multiple tracks can be selected by either holding the *shift* button and left clicking on each track or by holding shift and left clicking on a shared metadata term of consecutive tracks. In this manner, multiple tracks can be customized or moved at the same time. To deselect the tracks simply right click and press the button ``Deselect # tracks`` .

Track Color
~~~~~~~~~~~

Right clicking on ``annotation`` and ``numerical`` tracks will display ``Primary Color``, ``Secondary Color``, and ``Background Color`` which can all be customized using the color picker. For ``methylC`` tracks and ``categorical`` tracks the ``Color`` and ``Background`` of each class of elements (e.g. CG, CHG, and CHH) can be personalized. Additionally, for ``methylC``tracks the ``Read depth line color`` can be customized. 

Track Height
~~~~~~~~~~~~

For each track the height can be customized by right clicking on the track and typing in a number to the panel. At 20 pixels and below for ``numerical`` tracks the track will display as a heatmap. 

Track Display Mode
~~~~~~~~~~~~~~~~~~

For each ``numerical``, ``annotation``, or ``BAM`` track the display can be changed to ``DENSITY`` or ``FULL`` mode by right clicking on the track. 

Track Y-axis Scale
~~~~~~~~~~~~~~~~~~

For each ``numerical`` track the y-axis can be displayed in ``AUTO`` or ``FIXED`` mode by right clicking on the track. The ``AUTO`` mode will scale the axis based on numerical values in the immediate area of the view range. The ``FIXED`` mode allows the user to select ``a Y-Axis min`` or ``Y-axis max``. For values above the set max the ``Primary color above max`` can be set for easy viewing. For values below the set minimum the ``Primary color below min`` can bet set.  
