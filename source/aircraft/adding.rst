Adding Objects to Aircraft
==========================

Using the tetrahedron object file (tetrahedron.obj), we'll copy into the 
aircraft directory. By convention, miscellaneous (i.e., non-cockpit) objects should be
grouped in the ``objects`` subdirectory, under the aircraft's folder.

Then using `Plane Maker <https://developer.x-plane.com/manuals/planemaker/>`_,
select Standard -> Objects menu. This pops up a box where
you can add objects. On the right, there's a clickable button which pops up a file-selection
box. On the left, you can set the position of the object.

In this example, we want to place the object one meter above the center of gravity.
From the Plane Maker Weights & Balances page, we see that the COG if 2.9 feet back
from the reference point and .3 feet up.

So, we edit the object position to be "2.90" feet back, centered at "0", and moved up
"2.98" feet (one meter less 0.3 feet).

You can position the object relative other aircraft parts such as the Left Wing, or Vertical Stabilizer,
by selecting that as the aircraft reference.

.. image:: /images/plane_maker_tetrahedron.png

Note that *objects* have no effect on center of gravity or drag on the aircraft, they're just
visual elements. Flight characteristics are specified using Plane Maker (and/or modified by plugins).

(`2020 X-Plane Plane Maker Tutorial by danklaue on YouTube <https://www.youtube.com/playlist?list=PLXQZyRq30oEt1sbT_v-KAFRhrqrVNfWlT>`_)
(`2022 Animating in Blender Tutorial <https://www.youtube.com/watch?v=OvIuTE7lgys>`_)

xplane2blender  Scene properties -> Textures. Set (at least) Default to the file you created with Texture Paint / UV Editing
