Geometry Commands
=================

A geometric shape is formed by a set of vertices. To save space, as vertices may be shared, the OBJ8
format uses a level of indirection to define a shape.

For this, **Data Tables** are used.
At a high level, there is a list of vertices (``VT``) with detailed location information. Each ``VT`` record is a single point.
These are followed by a list of indices (``IDX``), where each index record points to one vertex.

After the Data Tables, shapes may be declared.
A geometric shape is described using a single ``TRIS`` command, which simple says, starting at index *offset*, every
three values point to three vertices formating a triangle. Continue through the index list for *count* records, making another
triangle out of every three vertices, and the result is the geometric shape. *Count* is always a multiple of 3.

Lines are drawn in a similar manner. A list of vertices (``VLINE``), with each being a single point (and color). The lines
are drawn with a single ``LINES`` command (which also uses index *offset* and *count*) referencing into the `VLINE` rather than
the `VT` vertices data table. *Count* is always a multiple of two. (This is rarely used in X-Plane.)

.. index:: Data Tables

Data Tables
-----------

Data Tables are used to store the object vertices.

First, the file contains a single ``POINT_COUNTS`` record
which indicates the size of each of the four tables. Then (for tables with entries) a set
of data records is listed, one entry per line (with the exception of ``IDX10`` records). 

.. index:: single: Commands; POINT_COUNTS
           single: POINT_COUNTS
           
| **POINT_COUNTS** ``vt_records   vline_records   vlight_records   index_records``

  Defines the number of entries in each of the four data tables. All values are non-negative integers.


.. index:: single: Commands; VT
           single: VT
           single: Triangle Vertex Table

| **VT** ``x y z   nx ny nz   s t``

  Single entry in the Triangle Vertex table. These are indexed starting from
  zero based on the record order. The eight floating point numbers represent a triplet coordinate location (x, y, z),
  a triplet normal (nx, ny, nz), and a pair forming a texture coordinate (s, t).

  Both s and t are valued 0.0 - 1.0 and represent relative position of that vertex in the UV map (e.g., the
  texture, the PNG file.) measured from the bottum left corner of the image.

  ``s`` is the x axis (.33 means the point is one-third in from the left side of the image), ``t`` is the y axis (.33 means
  the point is one-third up from the bottom of the image).

.. index:: single: Commands; VLINE
           single: VLINE
           single: Line Vertex Table

| **VLINE** ``x y z   r g b``

  Single entry in the Line Vertex table. These are indexed starting from
  zero, based on the record order. The six floating point numbers represent a triplet coordinate location (x, y, z),
  and a triplet color value (RGB, with values from 0.0 to 1.0).

.. index:: single: Commands; VLIGHT
           single: VLIGHT
           single: Light Vertex Table

| **VLIGHT** ``x y z   r g b``

  **[deprecated]** Single entry in the Light Vertex table. These are indexed starting from
  zero, based on the record order. The six floating point numbers represent a triplet coordinate location (x, y, z),
  and a triplet color value (RGB, with values from 0.0 to 1.0). Addionally:

     * If any color value is negative, the light is considered to be flashing.
    
     * If the color values are all 9.9, it is a pulsing red light.
    
     * If the color values are all 9.8, it is a strobe light.
    
     * If the color values are all 9.7, it is a traffic light.
    
    .. Warning:: The specialized light values based on the 9.x series may not be supported precisely in
                 future OBJ specs, and are not recommended. They are provided for compatibility.
    
.. index:: single: Commands; IDX
           single: Commands; IDX10
           single: IDX
           single: IDX10
           single: Index Table

| **IDX** ``n``
| **IDX10** ``n n n n n n n n n n``

  Define one, or ten, entries in the Index table. The index teable is used to refer to
  verticies in the Triangle or Line Vertex tables. Indices are zero based, and numbers are are based
  into the vertext tables. In other words, and index whose value is "4" can refer to the fifth row
  of the Triangle or Line Vertex table. ``IDX10`` is provided as a convenience to pack 10 indices onto one line.
  
  For example. The following tetrahedron  has 12 ``VT`` records, and 12 ``IDX`` records.::
  
    POINT_COUNTS    12      0       0       12
    
    VT  0.70655334  0.0012326837 -1.2262223    -0.40738449  0.57927406 -0.70603067     0.375  0.25
    VT  0           0.99888086   -0            -0.40738449  0.57927406 -0.70603067     0.625  0
    VT -1.4121311   0.0010700822 -0.0038604736 -0.40738449  0.57927406 -0.70603067     0.375  0
    VT  0.70655334  0.0012326837 -1.2262223     0.81663924  0.5771476   0.00098589214  0.375  0.25
    VT  0.70360208  0.0012326837  1.218384      0.81663924  0.5771476   0.00098589214  0.375  0.75
    VT  0           0.99888086   -0             0.81663924  0.5771476   0.00098589214  0.875  0.75
    VT -1.4121311   0.0010700822 -0.0038604736 -0.40893874  0.57600367  0.70780569     0.375  1
    VT  0           0.99888086   -0            -0.40893874  0.57600367  0.70780569     0.625  1
    VT  0.70360208  0.0012326837  1.218384     -0.40893874  0.57600367  0.70780569     0.375  0.75
    VT -1.4121311   0.0010700822 -0.0038604736  0.0000768  -1           0.00000009     0.125  0.75
    VT  0.70360208  0.0012326837  1.218384      0.0000768  -1           0.00000009     0.375  0.75
    VT  0.70655334  0.0012326837 -1.2262223     0.0000768  -1           0.00000009     0.125  0.5
    
    IDX10 0 1 2 3 4 5 6 7 8 9
    IDX 10
    IDX 11
  
    TRIS 0 12

  Note that ``IDX`` *n* values do not need to be in sequential order!
  
  .. image:: /images/tetrahedron.png
     :width: 250
     :alt: Tetrahedron        
             
  Note that ``IDX10`` entries *must* have ten values: use ``IDX`` entries for any
  remaining values.
  

Geometry Commands
-----------------

Geometry commands cause things to be drawn. They are either
entries from the Data Tables, using ``TRIS`` or ``LINES``.

.. index:: single: Commands; TRIS
           single: TRIS
           
| **TRIS** ``offset count``

  Describe a single geometry shape using a set of triangles. The vertices for the triangles are the
  set of vertices (in the ``VT`` Data Tables) as referenced, in order, by the set of `IDX` index records, starting
  and index *offset* continuing through *count* number of vertices.
  
  Every three vertices form a triangle, so the value of *count* must be divisible by 3.

  For example::

    IDX10 0 1  2  8  7  9  8 26  4  5
    IDX10 3 9 10 12 15 33 20  4 11  8

    TRIS 6 12

  Creates four triangles (12 / 3), with index numbers 8-26-4, 5-3-9, 10-12-15, 33-20-4. One would then
  look into the ``VT`` datatable to read the values for vertices at each of the index values to actually
  construct the triangles.
  

.. index:: single: Commands; LINES
           single: LINES
           
| **LINES** ``offset count``

  Describe a set of (possibly disconnected) lines. The vertices for *each* line segment are the
  set of vertices (in the ``VLINE`` Data Tables) as referenced, in order, by the set of `IDX` index records, starting
  and index *offset* continuing through *count* number of vertices.
  
  Every two vertices forms a line, so the value of *count* must be divisible by 2.

  For example::

    IDX10 0 1  2  8  7  9  8 26  4  5
    IDX10 3 9 10 12 15 33 20  4 11  8

    LINES 0 6

  Creates three lines (6 / 2), with index values 0-1, 2-8, and 7-9. One would then look into the ``VLINE`` datatable
  to read the values of vertices at each of the index values.

  Note this *does not* create a single line with five line segments, e.g., 0-1-2-8-7-9.
