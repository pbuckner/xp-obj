Introduction
============

**Objects** are three-dimensional things which can be placed & moved within the X-Plane environment.
They can be:

* Buildings, flags, trashcans, and other 3D objects displayed as part of X-Plane scenery

* Detailed rendering (e.g., rivets, guy-wires, windshields) and moving parts of aircraft
  (e.g., canopy, parking break, landing gear) and their 3D cockpit (e.g., displays, G1000 knobs, switches).

* Objects which can be placed and manipulated by plugins (e.g., deer, ships)

Yet, objects are just the things. You separately need to load and display them in
order to see them in X-Plane. When you're ready, see :doc:`adding`.

But first, you have to create your objects, see :doc:`creating`.

An **X-Plane Object** is a singular thing described by and wholly contained within a single X-Plane ``*.obj`` file.
The file itself may contain any number of 3D **geometric objects**, that is, any number of extruded and sliced
cubes, cylinders, cones, etc. For example, the single X-Plane Object for the Boeing 737-800 nose gear in
the file ``738nosegear.obj``, contains 16 geometric objects (sets of triangles).

 .. image:: /images/738nosegear.png
    :width: 350        

Typically, a 3D modelling tool such as `Blender <https://www.blender.org>`_ is used to create geometric objects
to compose the X-Plane object. The modelled object is then converted from native to X-Plane specific
format ("`OBJ8 <https://developer.x-plane.com/article/obj8-file-format-specification/>`_"), where it
is read and interpreted by the X-Plane simulator.

 .. image:: /images/738nosegear_blender.png

Some of the magic / complexity of X-Plane OBJ8 format relates to how the object is
represented within the X-Plane environment. This includes material (e.g., transparency) shadows,
level-of-detail, animation and manipulation through datarefs. Some of this complexity can be
added (and converted) within Blender, some complexity requires directly editing the converted OBJ file.

We'll cover:

* :doc:`/creating`
* :doc:`/adding`
* :doc:`/tools`
* :doc:`/obj8/reference`

About this documentation
------------------------
.. note::
   This is a work in progress, and may never get completed. I'm using this as an experiment to
   see if this method of documentation is useful.

* Targetted for X-Plane 12
   
* This is based off of `Laminar Research X-Plane Documentation <https://www.x-plane.com>`_.
  Much of the text is extracted from their public and copyrighted documentation.

* Comments and observations are collected from public forums (largely `X-Plane.org <https://forums.x-plane.org>`_),
  private emails, and conversions with other developers. We'll try to properly credit
  exceptional examples and insights.

* We'll (also) explicitly link to other useful references / videos
  which are owned and maintained separately from this reference.

* We'll use `XPPython3 <https://xppython3.rtfd.io>`_ examples when referencing code.

:doc:`changelog` lists current and previous documentation versions.
     
.. toctree::
   :hidden:
   :titlesonly:

   creating
   adding
   obj8/reference
   tools
   changelog
..
   document/pages
   document/pages
