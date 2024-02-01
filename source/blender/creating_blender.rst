Using Blender with X-Plane
==========================

See official `XPlane2Blender Docs <https://github.com/X-Plane/XPlane2Blender/wiki>`_, which
is partial update to the much older `XPlane2Blender Manual <https://xp2b-docs.gitbook.io/xplane2blender-docs>`_.
Both of these are old but some *very old* tutorials which may be helpful (may be relevant).

Once `installed using these instructions <https://github.com/X-Plane/XPlane2Blender/wiki/Installation>`_,
the XPlane2Blender plugin adds some extra features to Blender.

* :doc:`Export <exporting>` to OBJ8 format, with :doc:`error_logging`.

* :doc:`Animate <animating>` objects using X-Plane animation.

* :doc:`Setting light <lighting>` objects specific to X-Plane.

* :doc:`Setting attributes <attributes>` specific to X-Plane. 

Try our trivially easy three-step :doc:`"Hello Cube" example <hello_cube>`: to verify your installation.

Note that X-Plane and Blender use different 3D coordinate systems: X-Plane is "Y-up" and Blender is "Z-up". See :ref:`coordinate_system`

Useful Tutorials
----------------

I've found these particularly useful.

* Animation of a landing gear `Build it Better on YouTube <https://www.youtube.com/watch?v=zHnfMyeqB20>`_.

---

... what changes based on Scene type "Aircraft (part)", "Cockpit", "Scenery Object", "Instanced Scenery Object".

* Render Properties
* Scene Properties
* Object Properties
* Object Data Properties
* Material Properties

---



---

#. Go through each of the new properties & see if they make sense
#. Attempt to do XP stuff, like animation, particles, clear glass, etc.   

.. toctree::
   :hidden:
   :titlesonly:

   hello_cube
   error_logging
   animating
   lighting
   attributes
   particles
   exporting
