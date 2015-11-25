RKerning
========

.. image:: ../../images/RKerning.gif

Usage
-----

.. showcode:: ../../examples/objects/RKerning_00.py

.. code::

    < RKerning for Mailer-Regular >
     -123
     None
     [('X', 'emdash'), 
        ('K', 'v'),
        ('two', 'perthousand'),
        ('guilsinglleft', 'a'),
        ... etc.]

Description
-----------

``RKerning`` is a dictionary of kerning values. ``RFont`` makes a ``RKerning`` object when it is created and makes available as ``aFont.kerning`` attribute. The keys are tuples of the glyphs listed by their names: ``('T', 'e')``, ``('V', 'A')`` etc. ``None`` is returned if the pair does not exist, rather than raising an ``IndexError``. The parent of a kerning object is usually a Font.

Methods
-------

.. function:: add(value)

Add value to all kerning pairs.

.. function:: asDict()

Return the object as a plain dictionary.

.. function:: clear()

Clear all the kerning (why would you want to do that?).

.. function:: combine(kerningDicts, overwriteExisting=True)

Combine two or more kerning dictionaries. Overwrite exsisting duplicate pairs if ``overwriteExisting=True``.

.. function:: eliminate(leftGlyphsToEliminate=None, rightGlyphsToEliminate=None, analyzeOnly=False)

Eliminate pairs containing a left glyph that is in the ``leftGlyphsToEliminate`` list or a right glyph that is in the ``rightGlyphsToELiminate`` list. sideGlyphsToEliminate can be a string: ``'a'`` or list: ``['a', 'b']``. ``analyzeOnly`` will not remove pairs. it will return a count of all pairs that would be removed.

.. function:: explodeClasses(leftClassDict=None, rightClassDict=None, analyzeOnly=False)

Turn class kerns into real kerning pairs. Classes should be defined in dicts: ``{'O':['C', 'G', 'Q'], 'H':['B', 'D', 'E', 'F', 'I']}``. ``analyzeOnly`` will not remove pairs. it will return a count of all pairs that would be added.

.. function:: get(aPair)

Get a value. Return ``None`` if the pair does not exist.

.. function:: getAverage

Return average of all kerning pairs.

.. function:: getExtremes

Return the lowest and highest kerning values.

.. function:: getLeft(glyphName)

Return a list of kerns with ``glyphName`` as left character.

.. function:: getRight(glyphName)

Return a list of kerns with ``glyphName`` as right character.

.. function:: has_key(pair)

Returns True if it has the pair.

.. function:: implodeClasses(leftClassDict=None, rightClassDict=None, analyzeOnly=False)

Condense the number of kerning pairs by applying classes. This will eliminate all pairs containg the classed glyphs leaving pairs that contain the key glyphs behind. ``analyzeOnly`` will not remove pairs. It will return a count of all pairs that would be removed.

.. function:: importAFM(path, clearExisting=True)

Import kerning pairs from an AFM file. ``clearExisting=True`` will clear all exising kerning.

.. function:: interpolate(sourceDictOne, sourceDictTwo, value, clearExisting=True)

Interpolate the kerning between ``sourceDictOne`` and ``sourceDictTwo``. ``clearExisting`` will clear existing kerning first.

.. function:: items

Return a list of ``(pair, value)`` tuples.

.. function:: keys

Returns a lust of available pairs.

.. function:: minimize(minimum=10)

Eliminate pairs with value less than minimum.

.. function:: occurrenceCount(glyphsToCount)

Return a dict with glyphs as keys and the number of occurances of that glyph in the kerning pairs as the value ``glyphsToCount`` can be a string: ``'a'`` or list: ``['a', 'b']``

.. function:: remove(pair)

Remove a kerning pair.

.. function:: round(multiple=10)

Round the kerning pair values to increments of multiple.

.. function:: scale(value)

Scale all kernng pairs by value.

.. function:: swapNames(swapTable)

Change glyph names in all kerning pairs based on ``swapTable``::

    swapTable = {'BeforeName':'AfterName', }

.. function:: update(kerningDict)

Replace kerning data with the data in the given ``kerningDict``.

.. function:: values()

Return a list of kerning values.
