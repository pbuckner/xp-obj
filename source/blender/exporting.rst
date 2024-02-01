Exporting from Blender
======================

The result of exporting is one or more OBJ8 files, each of which will contain one X-Plane object.
There may be any number of "blender objects" within the X-Plane object.

Because there can be only one texture file associated with the OBJ8, *all* your blender objects must use the same
material.

You can use either the menu item, or buttons to export. Errors will be in :doc:`error_logging`.

Setting What to Export
----------------------
Each Collection (other than the top Scene Collection) can be exported to a separate file.

Each Object can be exported to a separate file.

However, you cannot nest exports. That is, if you're exporting a particular object or collection, that object cannot also
be a member of a collection being exported.

You mark a collection for export by selecting Scene Properties and opening the X-Plane section. You'll see a list of your
Collections. If none have been selected as "Root Collection", they'll be listed under "Other Collections". Otherwise you'll see the
selected and unselected Collections. In the following image, note that I've selected two collections, and have
not selected "Collection 2" to be exported.

  .. image:: /images/blender_collection_export.png
             :width: 350

Click on "Root Collection" checkbox to add this collection to the set to be exported. Each "Root Collection" will be exported to
a separate file.

You don't need to export the whole collection, you can export an object, which will cause it, and all child objects to
be exported. The technique is similar: Select Object Properties, then verify you've selected the correct object. Open the
X-Plane section and select "Root Object".

  .. image:: /images/blender_object_export.png
             :width: 350

Once you've identified one or more items to export, selecting "Export OBJs" from the Scene
Properties or selecting the Export->X-Plane Object from the menu will cause *all* selected
Root Collections and Root Objects to be exported to separate files.

Naming the Exported Object
--------------------------
Initially, your OBJ8 files will be named after what you are exporting. That is, ``Collection 2.obj``, if you've
selected Collection 2 as a Root Collection, or ``Cube.obj``, if you've selected that object to be a Root Object.

To export to a different filename, edit the "Name:" attribute under the X-Plane section of the Collection (under Scene Properties)
or Object (under Object Properites).

  .. image:: /images/blender_export_name.png
       :width: 350
    
The files will be exported to the same directory as the source blender file.

Export by Menu
--------------
    .. image:: /images/blender_export_menu.png 
               :width: 350
    

Export by Button
----------------

    .. image:: /images/blender_export_button.png 
               :width: 350
    


.. warning::
   Failure to export will be reported in the :doc:`Error log <error_logging>`. In some cases, *there is no other visible indication
   of failure*.


