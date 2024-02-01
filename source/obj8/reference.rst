OBJ8 File Format Reference
--------------------------

This is based off of Laminar Research's `OBJ8 File Format Specification <https://developer.x-plane.com/article/obj8-file-format-specification/>`_.

Basic file format
=================

OBJ8 files are text files (7-bit ASCII only) [#but_utf]_
that consists of records, one per line.
Any number of spaces or tabs are treated as white space. White space at the start (and end) of lines
is ignored.

Each record, i.e., each line, starts with a case-sensitve keyword (ignoring and leading white space, of course).
Fully blank lines are legal (after then 3-line header). Lines beginning with ``#`` are also treated as comments.

Lines which contain a single word (such as the Header lines) can include an in-line comment
if sepearated with a space. For example::

  OBJ # This is a comment

The format
is meant to be backward compatible: as new features are introduced, "old"
software should be able to safely ignore these new features.


.. _coordinate_system:

Coordinate System
=================

Distances are expressed in meters. The object's (0, 0, 0) point is the reference point for placing the object. That is,
if you say the object is at latitude 0.0, longitude 0.0 at ground level, then the object's (0, 0, 0) point is exactly
at that position.

X-Plane uses a Y-up 3D coordinate system, with +X to the east/right, and +Z to the south/back.

  +-------------------------+---------------------------+
  | +1 X is one meter right | -1 X is one meter left.   |
  +-------------------------+---------------------------+
  | +1 Y is one meter up    | -1 Y is one meter down.   |
  +-------------------------+---------------------------+
  | +1 Z is one meter back  | -1 Z is one meter forward.|
  +-------------------------+---------------------------+

.. note:: This is different from Blender's coordinate system which uses Z-Up. Fortunately, the XPlane2Blender plugin
          converts the coordinate systems, so "up" in Blender remains "up" in X-Plane. Right (positive X) is the same
          in both. Blender positive Y maps to X-Plane negative Z, so "pointing" something in Blender in a positive Y direction
          will result it in "pointing" in X-Plane the negative Z direction, which are both considered "forward".

          The OBJ8 file, of course, uses X-Plane coordinates.

              +-------------+-------------+------------------+
              | **X-Plane** | **Blender** | **\+ Direction** |
              +=============+=============+==================+
              |      X      |     X       |       Right      |
              +-------------+-------------+------------------+
              |      Y      |     Z       |         Up       |
              +-------------+-------------+------------------+
              |      Z      |    -Y       |     Backwards    |
              +-------------+-------------+------------------+
            
          
          
.. index:: Header, OBJ, 800, I
           single: Commands; I
           single: Commands; 800
           single: Commands; OBJ

File Header
===========

Header is *required* to be the first three lines of the file [#endings]_ (without blank lines or leading spaces.)::

   I
   800
   OBJ

Following the header are commands to define the objects, lights, and textures.
  
Commands
========

* :doc:`geometry`: Defining sets of triangles forming a geometric shapes, and lines (forming lines)
* :doc:`lights`: Defining light effects
* :doc:`animation`: Defining positioning changes to geometric shapes and lights, often due to dataref values.
* :doc:`textures`: Defining the texture (png file) used to overlay the object.
* :doc:`particles`: Defining particle emitters.

.. index:: single: Commands; MAGNET
           single: MAGNET
           
| **MAGNET** ``name  type  x y z  psi theta phi``

Attibutes
_________
| ATTR_LOD
| ATTR_LOD_draped
| ATTR_axis_detent_range
| ATTR_axis_detented
| ATTR_blend
| ATTR_cockpit
| ATTR_cockpit_device
| ATTR_cockpit_hud
| ATTR_cockpit_lit_only
| ATTR_cockpit_region
| ATTR_cull
| ATTR_diffuse
| ATTR_diffuse_rgb
| ATTR_draped
| ATTR_draw_disable
| ATTR_draw_enable
| ATTR_emission_rgb
| ATTR_hard
| ATTR_hard_deck
| ATTR_hud_glass
| ATTR_layer_group
| ATTR_layer_group_draped
| ATTR_light_level
| ATTR_light_level_reset
| ATTR_manip_axis_knob
| ATTR_manip_axis_switch_left_right
| ATTR_manip_axis_switch_up_down
| ATTR_manip_command
| ATTR_manip_command_axis
| ATTR_manip_command_knob
| ATTR_manip_command_knob2
| ATTR_manip_command_switch_left_right
| ATTR_manip_command_switch_left_right2
| ATTR_manip_command_switch_up_down
| ATTR_manip_command_switch_up_down2
| ATTR_manip_drag_axis
| ATTR_manip_drag_axis_pix
| ATTR_manip_drag_rotate
| ATTR_manip_drag_xy
| ATTR_manip_keyframe
| ATTR_manip_none
| ATTR_manip_noop
| ATTR_manip_toggle
| ATTR_manip_wheel
| ATTR_manip_wrap
| ATTR_no_blend
| ATTR_no_cockpit
| ATTR_no_cull
| ATTR_no_draped
| ATTR_no_hard
| ATTR_no_shadow
| ATTR_no_solid_camera
| ATTR_poly_os
| ATTR_reset
| ATTR_shade_flat
| ATTR_shade_smooth
| ATTR_shadow
| ATTR_shadow_blend
| ATTR_shiny_rat
| ATTR_solid_camera

Other
_____
| BLEND_GLASS
| COCKPIT_REGION
| DEBUG
| DECAL_LIB
| DITHER_ALPHA
| ENDIF
| EXPORT
| GLOBAL_cockpit_lit
| GLOBAL_luminance
| GLOBAL_no_blend
| GLOBAL_no_shadow
| GLOBAL_shadow_blend
| GLOBAL_specular
| GLOBAL_tint
| Global_specular
| IF
| NO_BLEND
| POINT_COUNTS
| RAIN_SCALE
| RAIN_scale
| REQUIRE_DRY
| REQUIRE_WET
| SLOPE_LIMIT
| SNOW_ALBEDO_LUMA
| SPECULAR
| SUPER_ROUGHNESS
| THERMAL_source
| THERMAL_texture
| TILTED
| TRIS
| WEATHER
| WEATHER_TRANSPARENT
| WIPER_param
| WIPER_texture
| smoke_black
| smoke_white

 http://developer.x-plane.com/tools/xptools/

----


.. [#but_utf]
   Laminar documentation says files are 7-bit ascii, but X-Plane ships with files encoded with UTF-8 and LATIN-1.
   I do not know the full extent of encodings which are acceptable.
   
.. [#endings]
   Technically, line endings are either single linefeed (``\n`` or 0x0a) if the first line of the header is ``I``,
   or carriage-return + linefeed (``\r\n`` or 0x0d0a) if the first line of the header is ``A``. Do yourself
   a favor and use ``I`` with simple newline.

.. toctree::
   :hidden:
   :titlesonly:

   geometry
   animation
   textures
   lights
   particles
