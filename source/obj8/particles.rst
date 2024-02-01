Particles and Emitters
======================

.. note::
    As of 2020, Particles and Emitters can be added *only* to
    :doc:`Aircraft </aircraft/adding>` and objects added via
    :doc:`Plugins </plugin/adding>`. They cannot be added to scenery (or, if added,
    the object works, but it will not emit anything.)


See also

* `X-Plane 11 Particle System <https://developer.x-plane.com/article/x-plane-11-particle-system/>`_
* `Particle Effects in X-Plane 11.30 <https://www.x-plane.com/2018/11/particle-effects-in-x-plane-11-30/>`_

The Particle System Brower is accessible from within the X-Plane simulator, under the Developer menu, and it's
use is described in the *X-Plane 11 Particle System*  article referenced previously.

.. index:: single: Commands; PARTICLE_SYSTEM
           single: PARTICLE_SYSTEM
  
| **PARTICLE_SYSTEM**  ``file.pss``

    The ``.pss`` file [#no_doc_pss]_ that defines the particle system for any EMITTER directives in this
    OBJ file. If particles are used, a particle system file *must be provided*. An OBJ with
    a ``PARTICLE_SYSTEM`` directive but no ``EMITTER`` directives results in a warning, not an error.
  
    Only one ``PARTICLE_SYSTEM`` is allowed per OBJ file. The file is located *relative the OBJ file*: You cannot
    use a "global" resource such as ``Resources/effects/aircraft_system.pss``. (*And*, because the particle system
    file references a PNG file, make sure that's in the same directory!)
  
.. index:: single: Commands; EMITTER
           single: EMITTER
           
| **EMITTER** ``name  x y z  psi theta phi  [index]``

    Defines a particle emitter of the given *name*. Name must be found in the ``PARTICLE_SYSTEM`` file.

    (x, y, z) locates the position of the emitter. (psi, theta, phi) indicated the degrees of roll, pitch, and heading.

    *index* is optional and, if left out, is assumed to be 0.

---

.. [#no_doc_pss] As of X-Plane 12, there is no documentation related to format of a ``.pss`` file.


             
