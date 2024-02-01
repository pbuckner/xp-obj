X-Plane Lights and Blender
==========================

Named Lights
------------

To add a :ref:`named light <light_named>`, add a Light object to your scene and then set the
name of the light object to one of the predefined values (See :doc:`/obj8/lights`.)

Type in a bad name, and blender will tell you. X-Plane omni-directional lights need to be
created as Blender "Point" lights. X-Plane directional lights need to be created as Blender "Spot" lights.
Select the wrong type and Blender will tell you.

  .. image:: /images/blender_light_named.png
     :width: 350

Blender will include a ``LIGHT_NAMED`` command in the export OBJ8 file.

Parameterized Lights
--------------------

Parameterized lights can be added like Named Lights, but (current) XPlane2Blender plugin does not
allow you to set the parmeters from within Blender. The correct # of parameters for the particular
parameterized light will be written into the OBJ8 file on export, but they'll have default values.

You'll need to hand edit these values.





