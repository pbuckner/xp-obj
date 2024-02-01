Textures
========

There can be only one texture per OBJ8 file for all the defined objects within the file. But, there can be
different texture files, used in different circumstances.

In the simplest case the default texture, which should point to a PNG file. If no texture is defined or left
blank, the object
can still be used but will have a light grayish appearance (depending on in-sim lighting):

.. index:: single: Commands; TEXTURE
           single: TEXTURE

| **TEXTURE** ``filename``

This is also represents the "daytime" (albedo) texture for the object.

.. index:: single: Commands; TEXTURE_LIT
           single: TEXTURE_LIT

| **TEXTURE_LIT** ``filename``

If defined, this represents the "lit" (emissive) texture for the object.

.. index:: single: Commands; TEXTURE_NORMAL
           single: TEXTURE_NORMAL

| **TEXTURE_NORMAL** `filename``

If defined, and per-pixel lighting has been enabled, this contains the specular strength in the alpha
channel. (TBA)


.. index:: single: Commands; TEXTURE_CONTROL
           single: TEXTURE_CONTROL

| TEXTURE_CONTROL

.. index:: single: Commands; TEXTURE_DRAPED
           single: TEXTURE_DRAPED

| TEXTURE_DRAPED

.. index:: single: Commands; TEXTURE_DRAPED_NORMAL
           single: TEXTURE_DRAPED_NORMAL

| TEXTURE_DRAPED_NORMAL

.. index:: single: Commands; TEXTURE_MAP
           single: TEXTURE_MAP

| TEXTURE_MAP

.. index:: single: Commands; TEXTURE_TERRAIN
           single: TEXTURE_TERRAIN

| TEXTURE_TERRAIN

.. index:: single: Commands; NORMAL
           single: NORMAL

| NORMAL

.. index:: single: Commands; NORMAL_METALNESS
           single: NORMAL_METALNESS


           
| NORMAL_METALNESS

https://www.youtube.com/watch?v=x_S9NosDYIM on some metal/ normal[O

.. index:: single: Commands; NORMAL_TRANSLUCENCY
           single: NORMAL__TRANSLUCENCY

| NORMAL_TRANSLUCENCY


