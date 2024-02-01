Hello Cube Example
==================

This is the *absolute minimum* you need to do to export an object -- in this case the ubiquitous Blender Square:

#. **Save your blender file**. You cannot export if it's not been saved

#. **Delete Blender-provided Lights and Cameras**. X-Plane doesn't use cameras, and
   lights are configured differently (:doc:`lighting`).

   .. image:: /images/blender_hello_delete_camera.png
              :width: 250

#. **Set what to export**. One or more collections or objects. In this case, you have one Collection (called "Collection")
   and one Object (called "Cube"). Select the object, then Object Properties. Open the X-Plane section and select "Root Object".
   (Details in :doc:`exporting`.)

   .. image:: /images/blender_hello_select_root.png
              :width: 250
              

#. **Select Export Menu** from the File->Export->X-Plane Object menu.

The file will be named ``Cube.obj`` (because that's the object you exported) and will be located in the same directory
as your Blender file.

Drop the resulting OBJ8 file onto ObjView (see :doc:`/tools`), and see the Cube!
      
