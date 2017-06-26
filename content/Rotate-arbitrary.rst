Rotate arbitrary
################

:date: 2012-07-21 16:13
:tags: open source, python
:category: python
:author: Simon

Another way to rotate by arbitrary values.

You can in python 2.x - just str.encode(“rot13”) - but for other
rotations you could use the following (for ascii):

.. code-block:: python

    from string import ascii_uppercase as uc, ascii_lowercase as lc, maketrans


    def rot_func(text, encode=True, rotate=13):
        letters = uc + lc
        rot = "".join((x[:rotate][::-1] + x[rotate:][::-1])[::-1] for x in (uc,lc))
        src, trg = (letters, rot) if encode else (rot, letters)
        trans = maketrans(src, trg)
        return text.translate(trans)

    text = "Text to ROT"
    encoded = rot_func(text)
    decoded = rot_func(encoded, encode=False)

    print("""
    Text:\t{text}
    Encode:\t{encoded}
    Decode:\t{decoded}
    """.format(**locals()))

`Github gist`_

.. _Github gist: https://gist.github.com/3156361
