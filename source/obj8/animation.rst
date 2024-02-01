Animation Commands
==================

Animation consists of:

* Show/Hide an object -- usually in response to a dataref
* Rotating an object -- either to a new set position, or changing based on the value of a dataref
* Translating (i.e., moving) an object -- either to a new set position, or changing based on the value of a dataref

An X-Plane OBJ8 file may consist of multiple geometric objects, each of these objects can be
controlled separately, by specifying the :doc:`geometry` controlled by the animation sequence.

The specified geometry will have its own zero point (0, 0, 0), through which the axis of rotation
will pass. Each animation will provide a unit vector (x, y, z), around with the object will rotate using the
``ANIM_rotate`` or ``ANIM_rotate_begin`` commands.

The amount and direction of rotation is specified by the ``ANIM_rotate`` or ``ANIM_rotate_key`` commands (where "amount" may be
a fixed amount or changes with a dataref).

Translation works in a similar manner. The geometic object is moved to a new location relative its starting position using ``ANIM_trans``
or ``ANIM_trans_key``.

Translation and rotation can be combined for the same geometric object.


Control
-------

.. index:: single: Commands; ANIM_begin
           single: Commands; ANIM_end
           single: ANIM_begin
           single: ANIM_end

| **ANIM_begin**
| **ANIM_end**

Animation occurs between ``ANIM_begin`` and ``ANIM_end``
Within this begin/end block should be a Geometry command (commonly ``TRIS``) to indicate *what* is
being animated.

There can be any number of being/end blocks, and blocks can be nested within other animation blocks (each
with a Geometry command.)

Show / Hide
-----------

.. index:: single: Commands; ANIM_hide
           single: ANIM_hide

| **ANIM_hide** ``v1 v2  [dataref]``

Hide the object being animated, when the dataref's value is between ``v1`` and ``v2`` (inclusive). The
object still exists and may have it's state updated, it just won't be visible (it will continue rotating,
for example.) This does nothing if the animation is not being shown.

.. index:: single: Commands; ANIM_show
           single: ANIM_show

| **ANIM_show**  ``v1 v2  [dataref]``

Show the object being animated, when the dataref's value is between ``v1`` and ``v2`` (inclusive).
This does nothing if the animation is not hidden. Note that show/hide are not counted, e.g., if you
hide twice and show once, the drawing is resumed.

In case of show/hide overlap commands, the commands are executed in order, with the later commands taking
effect::

  ANIM_hide 20 70 sim/time/total_running_time_sec
  ANIM_show 30 40 sim/time/total_running_time_sec
  ANIM_hide 35 45 sim/time/total_running_time_sec
  ANIM_show 60 65 sim/time/total_running_time_sec

Would result in the following:

.. table:: 
  :align: left

  +-------+-----+----+
  |Action |From | To |
  +=======+=====+====+
  | Show  | 0   | 20 |
  +-------+-----+----+
  | Hide  | 20  | 30 |
  +-------+-----+----+
  | Show  | 30  | 35 |
  +-------+-----+----+
  | Hide  | 35  | 60 |
  +-------+-----+----+
  | Show  | 60  | 65 |
  +-------+-----+----+
  | Hide  | 65  | 70 |
  +-------+-----+----+
  | Show  | 70+ | 70 |
  +-------+-----+----+

Rotation
--------

"Rotation" in this context is really *rate of rotation*. That is, the amount of rotation relative the change
in the dataref. (It is
possible to set the rate to 0 which results in an object simply being drawn in that rotated angle. This is
described at the end of the *Simple Rotation* section below.)

There are two different commands to set up object rotation:

* **Simple Rotation** using ``ANIM_rotate``, where the object rotates linearly based on value of a
  dataref, or is rotated to a fixed position.
* **Keyframe Rotation** using ``ANIM_rotate_key``, and related commands, allowing a variable speed of rotation.

Simple Rotation
_______________

.. index:: single: Commands; ANIM_rotate
           single: ANIM_rotate
           
| **ANIM_rotate** ``x y z   r1 r2  v1 v2  [dataref]``

This is simple rotation. The axis of rotation (x, y, z) should form a unit length vector (x**2 + y**2 + z**2 == 1.0).
For example, (0, 1, 0) points straight up.

Angle of rotation is from r1 degrees to r2 degrees, scaled between v1 and v2, with the current rotational value being
determined by the dataref. Positive rotation is counterclockwise, when viewed from above (the rotation axis vector).

Rotations occur around the object's origin (0, 0, 0). If you need to point to be something other than the origin, you need to (also)
use :ref:`Animation Translation <ANIM_trans>`.

This *does not mean* the object merely starts at ``r1`` and ends at ``r2``. Nor does it mean there is no rotation
if the dataref returns a value below ``v1`` or above ``v2``. (Read on for explanation.)

Simple example::

  r1 = 0.0
  r2 = 360.0
  v1 = 0.0
  v2 = 10.0
  dataref = 'sim/time/total_running_time_sec'

Object will rotate counterclockwise. For each 10.0 (v2 - v1) change in the dataref,
it will execute 360.0 rotation (r2 - r1).
So, put another way, as ``total_running_time_sec`` increases, the object will rotate at
a rate of 36 degrees per second.

This is identical to::

  r1 = 45.0
  r2 = 81.0
  v1 = 1.0
  v2 = 2.0
  dataref = 'sim/time/total_running_time_sec'

36 degrees counterclockwise rotation per 1.0 unit change of dataref value.

Using::

  r1 = 10
  r2 = -20
  v1 = 5
  v2 = 10
  dataref = 'sim/time/total_running_time_sec'

30 degree clockwise rotation per 5 seconds.

Note that the rotation also never stops (in this example). As the dataref value increases over ``v2`` (or decreases
below ``v1``) the computed angle of rotation may exceed 360 degrees or go negative, which merely continues the rotation. Also,
even though ``v1`` is 5, rotation starts *immediately* (i.e., it doesn't wait to begin rotation until running time
is 5 seconds.)

For datarefs which have simple ranges, such as ``sim/cockpit2/engine/actuators/throttle_ratio[0]``, which varies
between 0.0 and 1.0, rotation occurs only as the throttle is moved. The following example would rotate the object
clockwise from 0 to 90 degrees clockwise, reflecting the state of the throttle from 0.0 to 1.0::

  r1 = 0
  r2 = -90
  v1 = 0.0
  v2 = 1.0
  dataref = 'sim/cockpit2/engine/actuators/throttle_ratio[0]`

Again, because X-Plane doesn't ignore dataref values above or below ``v1 v2``, it will extrapolate rotational value.
The following example will *also* rotate the object 90 degrees from start to finish, but, when ``v1 == 0``, the
object will start rotated 22.5 degrees *counterclockwise*. Because the rate of rotation is -22.5 degrees per ``v2-v1 = .25``
change in dataref, and at ``v1``, the rotational value is ``r1`` or zero.::

  r1 = 0
  r2 = -22.5
  v1 = .25
  v2 = .5
  dataref = 'sim/cockpit2/engine/actuators/throttle_ratio[0]`

The dataref is optional. If you leave it out (or specify a bad dataref or "none" or "no_ref"),
the object is rotated "permanently". For example,::

  ANIM_rotate 0 1 0   90 90  0 0

Draws the objected rotated 90 degrees. This can be useful where the object vertices were set up with the wrong
rotation. Rather than change the object in the 3D modelling application, and re-generate the vertices,
you can change it "at the last minute" using the command.

See also the old `"Fun with Animation" Developers note <https://developer.x-plane.com/2006/01/fun-with-animation/>`_.

Keyframe Animation
__________________

With Keyframe Animation, you'll specific a set of keyframes using ``ANIM_rotate_key``,
allowing you to specify a non-linear relationship between a dataref and rotation values.

These keyframes are surrounded by ``ANIM_rotate_begin`` and ``ANIM_rotate_end``.


.. index:: single: Commands; ANIM_rotate_begin
           single: Commands; ANIM_rotate_end
           single: ANIM_rotate_begin
           single: ANIM_rotate_end

| **ANIM_rotate_begin** ``x y z  dataref``
| **ANIM_rotate_end**

These commands do not take any parameters. They need to be nested within ``ANIM_begin`` and ``ANIM_end``.
(can they be nested? TBA)

Like ``ANIM_rotate``, ``ANIM_rotate_begin`` requires an axis of rotation (x, y z) and a dataref. The mapping for dataref value to degrees of rotation is specified explicitly using one or more ``ANIM_rotate_key`` commands.

.. index:: single: Commands; ANIM_rotate_key
           single: ANIM_rotate_key

**ANIM_rotate_key** ``value angle``

Each ``ANIM_rotate_key`` provides a mapping from the dataref value specified using ``ANIM_rotate_begin`` and degrees of rotation.

For example::

     ANIM_rotate_begin 0 1 0 sim/time/total_flight_time_sec
       ANIM_rotate_key 0 0
       ANIM_rotate_key 5 180
       ANIM_rotate_key 10 270
       ANIM_rotate_key 15 315
       ANIM_rotate_key 20 337
       ANIM_rotate_key 30 360
       ANIM_rotate_key 35 360
       ANIM_rotate_key 40 337
       ANIM_rotate_key 45 315
       ANIM_rotate_key 50 270
       ANIM_rotate_key 55 180
       ANIM_rotate_key 60 0
     ANIM_rotate_end

Will rotate the object around its vertical axis (0, 1, 0), using the ``total_flight_time_sec`` dataref.
For data ref values between 0 and 5 seconds, the rotation rate will be 180 / 5 seconds. For values between 5 and 10,
the rate is 90 degrees / 5 seconds, etc. The full example above will rotate an object 360 degrees, moving quickly, then
slowing down as it reaches a complete rotation. Then, it slowly reverses direction, speeding up as in completes the
return rotation. The complete action takes 60 seconds.

The ``total_flight_time_sec`` dataref, of course, will exceed 60 seconds. When the dataref value exceeds to key frame value,
the last rate is used. In this example, the object will continue to rotate at its final rate: 180 degrees per 5 seconds. When the dataref
value is less than the first key frame value, the first rate is used.

The keyframes don't appear to *need to be* in ascending order by ``value``. The frames are sorted by value and then the
mapping is performed.

If you want it to stop, you can add a final keyframe with the same value as the previous. This will change the rotation rate
to 0::

       ...
       ANIM_rotate_key 45 315
       ANIM_rotate_key 50 270
       ANIM_rotate_key 55 180
       ANIM_rotate_key 60 0
       ANIM_rotate_key 65 0
     ANIM_rotate_end

Alternativly, you can loop the animation using ``ANIM_keyframe_loop``.
  
.. index:: single: Commands; ANIM_keyframe_loop
           single: ANIM_keyframe_loop

**ANIM_keyframe_loop** ``loop``

Add ``ANIM_keyframe_loop`` at the bottom of a set of keyframes and the set of rotations will be repeated modulo the ``loop`` value.
So ending our previous example with::

       ANIM_rotate_key 45 315
       ANIM_rotate_key 50 270
       ANIM_rotate_key 55 180
       ANIM_rotate_key 60 0
       ANIM_rotate_key 65 0
       ANIM_keyframe_loop 65
     ANIM_rotate_end
   
Will result in the object rotating 360 degrees one way, then back, then forward, then back etc, because the dataref
value for ``total_flight_time_sec`` is divided by 65, and the result is used to determine the new rate.

.. _ANIM_trans:

Translation
-----------

Translation simply moves the geometric object.

.. index:: single: Commands; ANIM_trans
           single: ANIM_trans

**ANIM_trans** ``x1 y1 z1  x2 y2 z2  v1 v2 [dataref]``

The first (x, y, z) set of coordinates indicate the starting position of the move (relative dataref `v1`), so
(0, 0, 0) leaves the object in its initial position.

The second (x, y, z) set of coordiates indicate the ending position of the move (relative dataref `v2`), so
(0, 10, -1) moves the object 10 meters in the y direction ("up"), and -1 meter in the z direction
(for aircraft, towards the front).

Start the object one meter up (``v1==0``) and move the object up 10 additional meters per 60 seconds of flight time, forever.::

    ANIM_trans 0 1 0   0 10 0   0 60   sim/time/total_flight_time_sec


Move the object along the X axis (e.g., to the right side of an aircraft) forever at 10 meters per minute::

    ANIM_trans 0 0 0   10 0 0   0 60   sim/time/total_flight_time_sec

Move the object along the Y axis (e.g., backwards from an aircraft) forever at 10 meters per minute (written
as one meter per six seconds)::

    ANIM_trans 0 0 0   0 0 1   0 6 sim/time/total_flight_time_sec

Without a dataref, you can move it once. To place the object 10 meters in front and 1 meter above the initial
position::

    ANIM_trans   0 1 -10   0 1 -10   0 0

One note about not using a dataref: Effectively, it sets the value to 0, but all the rest of the calculations
are performed so the following will actually move the object 5 meters forward::

    ANIM_trans   0 1 0   0 1 -10   -1 1

Do your future debugging self a favor: If you going to not use a dataref,
set ``x1, y1, z1 == x2, y2 z2`` and ``v1, v2 == 0, 0``.

If using both translation and rotation, order is significant! If you translate first, the object is moved to
its new location, and then its rotation around the (new) zero point. That is, it would allow you to have
a rotation object moved from above the center of your plane to be out on the end of the wing, yet still rotate
around the object's center.

If you rotate first and then translate, the object starts rotation, but instead of rotating around the object's
center, you'll be rotating around the point translated away from the center point. Instead of a beacon on your wing tip,
it's a beacon on the end of a helicopter rotor.
 
| ANIM_trans_begin [dataref]
| ANIM_trans_end
| ANIM_trans_key value x y z
  
