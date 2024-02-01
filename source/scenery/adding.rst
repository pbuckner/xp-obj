Adding Objects to Scenery
=========================

Adding an object to scenery requires you to add the relevant information
to a `DSF <https://developer.x-plane.com/article/dsf-file-format-specification/>`_ file. While it
is possible to create one by hand, it's vastly easier to simply use
`Word Editor (WED) <https://developer.x-plane.com/manuals/wed/>`_.

The idea is to create a scenery package which includes your custom object(s) and
information about the placement of these objects.

#. First, under your main X-Plane directory, create a new package (e.g., "Tetrahedron Package")
    under the ``Custom Scenery`` folder. Then, create a subfolder called ``objects``, and then
    copy all custom objects you want to use into that folder::

        <X-Plane>/
        └─── Custom Scenery/
             └─── Tetrahedron Package/
                  └─── objects/
                       └─── tetrahedron.obj

    The subfolder *does not* need to be called ``objects``. WEB will look in all subdirectories for
    object files... and subdirectories of subdirectories, so you can group your objects any way you
    like.
    
#. Start WED, make sure it's pointing to your X-Plane Root (select "CHOOSE X-Plane Folder").

#. You'll see your package in the list.

   .. image:: /images/wed_open_tetrahedron.png
              :width: 350
              :alt: WED package selection        

   Select and Open your package. (BTW, there's not special about calling it "Package".)

#. The main window appears. Note your object(s) will be listed under Local->objects
   in the Library Pane (upper left).

   .. image:: /images/wed_local_library.png
              :width: 350
              :alt: WED local library object list

   ...or Local->foobar, if that's what you named your subdirectory.

#. Now you need to place your object on the map. This is easy:

    * Select the object you want to add. Note the select toolbar icon switches to the Building (which
      represents all objects.)
    * Click on the map where you want the object to appear. Note a copy of the object appears in the
      Hierarchy Pane (upper-right listing).
    * Make any edits, such as heading and elevation in the details box in Attributes Pane (lower right).
    
   .. image:: /images/wed_tetrahedron.png
             :alt: Object placement

One complication: it's unlikely the map will be centered on where you want to place the object, so a
simple "click on the map" isn't so simple.

If you're familiar with editing Airports, then you'll know you can import the airport and update the map to show the airport environs.
Without an airport, you'll need to either zoom & scroll the map to the correct location. This can be tedious and difficult.

Alternatively, do it this way:

#. Add your object *anywhere*. Just click anywhere on the map.

#. In the resulting Attributes Pane, *edit the latitude and longitude* of your inserted object. In our example,
   we set these to the geographic center of the United States.

#. Select menu View->Zoom Selected and the map will update to show your currently selected object. From there
   you can further refine the location or add more objects.


Finally,

* **Save** your work -- this merely saves an XML file allowing you to continue editing this package.
* **Export to Scenery** -- this exports the binary DSF file in a form suitable for the simulator.

Because it's so easy to align and rotate objects, I added a set of them encircling the location.

.. image:: /images/tetrahedral_circle.png
           
