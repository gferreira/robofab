RGlyph
======

.. image:: ../../images/RGlyph.gif

Usage
-----

.. showcode:: ../../examples/objects/RGlyph_00.py

Description
-----------

The ``RGlyph`` object represents a glyph, its parts and associated data. In FontLab ``RGlyph`` talks directly to a glyph in an open font. In NoneLab the ``RGlyph`` refers to data read from (and written to) a specific glif file in a UFO. ``RGlyph`` can be used as a list of ``RContour``. When ``RGlyph`` is obtained from a RoboFab font object (see examples), the font is the parent object of the glyph.

Attributes
----------

.. attribute:: components

A list of the :doc:`Components <RComponent>` in this glyph.

.. attribute:: anchors

A list of the :doc:`Anchors <RAnchor>` in this glyph.

.. attribute:: len(aGlyph)

The number of contours.

.. attribute:: aGlyph[index]

Get the :doc:`Contour <RContour>` object at index.

.. attribute:: width

The horizontal advance width of the glyph.

.. attribute:: leftMargin

The left margin of the glyph.

.. attribute:: rightMargin

The right margin of the glyph.

.. attribute:: name

The glyph name.

.. attribute:: unicode

The unicode value for this glyph, integer.

.. attribute:: note

A place for a short string, a note about this glyph.

.. attribute:: unicodes

A list of unicodes value for this glyph. Not all applications and editors support multiple unicode values for a glyph. Assume that ``glyph.unicode == glyph.unicodes[0]``.

.. attribute:: box

The bounding box. The values are ``(xMin, yMin, xMax, yMax)``. Note: these values represent the actual measurements of the shape of the glyph. They're usually different from the rectangle described by ``glyph.width`` / ``font.info.unitsPerEm``.

.. attribute:: + - *

Math operators work on glyphs.

.. seealso::  :doc:`how to glyphmath <../howtos/glyphmath>`.

.. attribute:: lib

The glyph's lib, an :doc:`RLib <libs>`.

.. seealso:: :doc:`how to use the lib <../howtos/use_lib>`.

.. attribute:: psHints

A :doc:`PostScriptGlyphHintValues <psHintsGlyph>` object with all glyph level PostScript hints, vertical and horizontal.

Attribute examples
------------------

.. showcode:: ../../examples/objects/RGlyph_01.py

.. code::

    230
    Adieresis
    [123, 345]
    1000
    4

Methods
-------

.. function:: getParent()

Return the parent of this glyph, the font object it belongs to. The method returns ``None`` if there is none.

.. function:: appendComponent(glyphName, (offsetX=0, offsetY=0), (scaleX=1, scaleY=1))

Add a component to the glyph. Optional values for ``offset`` and ``scale``.

.. function:: appendContour(aContour)

Add a contour to the glyph.

.. function:: removeComponent(componentObject)

Remove a component from the glyph.

.. function:: appendGlyph(aGlyph, (offsetX=0, offsetY=0))

Add a whole glyph. This adds all the contours, anchors and components to the glyph.

.. function:: appendAnchor(name, position)

Create a new anchor in this glyph with name at position.

.. function:: removeAnchor(anchor)

Remove this anchor from the glyph. This only works if the glyph does not have anchors with duplicate names in exactly the same location with the same mark.

.. function:: autoUnicodes()

Try to find unicode values for this glyph. This method tries to match the glyph name to a known value.

.. function:: copy()

Returns a deep copy of this glyph. That means that all parts of the glyph: contours, components, anchors etc. are duplicated.

.. function:: correctDirection()

Correct the direction of all contours in this glyphs.

.. function:: autoContourOrder()

Automatically order the contours based on (in this order):

1. the point count of the contours
2. the segment count of the contours
3. the ``x`` value of the center of the contours
4. the ``y`` value of the center of the contours
5. the surface of the bounding box of the contours

.. function:: pointInside((x, y))

Returns ``True`` if the point is inside the "black" area of the glyph or ``False`` if the point is inside the "white" area of the glyph.

.. function:: draw(aPen)

Get this glyph to draw itself with the pen on offer.

.. function:: drawPoints(aPointsPen)

Get this glyph to draw itself with the points pen on offer. For differences between ``Pen`` and ``PointsPen`` see here :doc:`Pens <pen>`.

.. function:: getPen()

Returns an appropriate ``Pen`` object to draw in this glyph.

.. function:: getPointPen()

Returns an appropriate ``PointPen`` object to draw in this glyph.

.. function:: interpolate(factor, minGlyph, maxGlyph, suppressError=True, analyzeOnly=False)

Make this glyph the interpolation between ``minGlyph`` and ``maxGlyph`` by factor. When ``suppressError`` is ``True`` (the default value) this method will not complain if the interpolation is not possible. When ``analyzeOnly`` is ``True`` (default is ``False``), this method will only analyze if the interpolation is possible and provide a report if something is wrong.

.. seealso:: :doc:`how to interpolate <../howtos/interpolate>`.

.. function:: isCompatible(anotherGlyph, report=True)

Returns ``True`` if the glyph has a compatible point structure as ``anotherGlyph``. When report is ``True``, ``isCompatible`` also returns a report on what the problems could be. 

.. seealso:: :doc:`how to interpolate <../howtos/interpolate>`.

.. function:: isEmpty()

Returns ``True`` when the glyph does not contain any contours, components or anchors.

.. function:: move(x, y), contours=True, components=True, anchors=True)

Move a glyph's items that are flagged as ``True``.

.. function:: scale((x, y), center=(0, 0))

Scale the glyph by `x` and `y`. Optionally set the center of the scale.

.. function:: rotate(angle, offset=None)

Rotate the glyph by ``angle`` (in degrees). Optionally set an ``offset`` value.

.. function:: skew(angle, offset=None)

Skew the glyph by ``angle`` (in degrees). Optionally set an ``offset`` value.

.. function:: rasterize(cellSize=50, xMin=None, yMin=None, xMax=None, yMax=None)

Slice the glyph into a grid based on the cell size. It returns a list of lists containing bool values that indicate the black (``True``) or white (``False``) value of that particular cell. These lists are arranged from top to bottom of the glyph and proceed from left to right. This is an expensive operation!

Method examples
---------------

.. showcode:: ../../examples/objects/RGlyph_02.py

FontLab
-------

Methods
^^^^^^^

Glyph methods only available in FontLab.

.. function:: removeOverlap

Remove overlap in this glyph.

.. function:: naked

Return the wrapped FontLab glyph object itself. This can be useful if you want to set very specific values in the FontLab font that aren't wrapped or handled by RoboFab objects.

.. function:: update

Tell FontLab to update all references to this glyph. Call this after you've changed something in the glyph object and you want these changes to be seen in the application. If you're calling ``glyph.update()`` a lot, for instance in a loop, consider calling it only once after the loop is done. You can also call ``font.update()`` if you've changed several glyphs at once. Calling ``update()`` makes a script slower.

.. function:: getVGuides

Return a list of wrapped vertical guides in this ``RGlyph``.

.. function:: getHGuides

Return a list of wrapped horizontal guides in this ``RGlyph``.

.. function:: appendVGuide(x)

Add a vertical guide at ``x`` in this ``RGlyph``.

.. function:: appendHGuide(y)

Add a horizontal guide at ``y`` in this ``RGlyph``.

.. function:: clearVGuides()

Remove vertical guides from this ``RGlyph``.

.. function:: clearHGuides()

Remove horizontal guides from this ``RGlyph``.

Useful
------

.. showcode:: ../../examples/objects/RGlyph_03.py
