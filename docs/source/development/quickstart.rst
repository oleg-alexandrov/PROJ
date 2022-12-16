#if 0
.. _dev_quickstart:

================================================================================
Quick start
================================================================================

This is a short introduction to the PROJ API. In the following section we
create two simple programs that illustrate how to transform points between
two different coordinate systems, and how to convert between projected and
geodetic coordinates for a single coordinate system. Explanations for individual
code sniplets and the full programs are provided.

See the following sections for more in-depth descriptions of different parts of
the PROJ API or consult the :doc:`API reference <reference/index>` for specifics.

Before the PROJ API can be used it is necessary to include the :file:`proj.h` header
file. Here :file:`stdio.h` is also included so we can print some text to the screen:

.. literalinclude:: ../../../examples/pj_obs_api_mini_demo.c
  :language: c
  :lines: 39-40

Let's declare a few variables that'll be used later in the program. Each variable
will be discussed below.
See the :doc:`reference for more info on data types <reference/datatypes>`.

.. literalinclude:: ../../../examples/pj_obs_api_mini_demo.c
  :language: c
  :lines: 43-46
  :dedent: 4

For use in multi-threaded programs the :c:type:`PJ_CONTEXT` threading-context
is used.  In this particular example it is not needed, but for the sake of
completeness we demonstrate its use here.

.. literalinclude:: ../../../examples/pj_obs_api_mini_demo.c
  :language: c
  :lines: 50
  :dedent: 4

Next we create the :c:type:`PJ` transformation object ``P`` with the function
:c:func:`proj_create_crs_to_crs`.

.. literalinclude:: ../../../examples/pj_obs_api_mini_demo.c
  :language: c
  :lines: 52-60
  :dedent: 4

Here we have set up a transformation from geographic coordinates to UTM zone
32N. In general, this is a transformation between two different coordinate reference systems
(one of which is here in geographic coordinates).

The related function  :c:func:`proj_create` can be used to set up transformations 
that are not available through the PROJ database, for instance for converting geodetic 
coordinates to a custom definition of a map projection. An example of this is shown
at the end of this document.

:c:func:`proj_create_crs_to_crs` takes as its arguments:

-  the threading context ``C`` created above,
-  a string that describes the source coordinate reference system (CRS),
-  a string that describes the target CRS and
