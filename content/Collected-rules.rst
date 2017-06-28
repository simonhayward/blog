Collected rules
###############

:date: 2017-06-28 23:03
:tags: python, quotes, linux
:author: Simon


Taken from the excellent book `The Practice of Programming`_ as relevant now as it was back when it was published.


Style
-----

* Use descriptive names for globals, short names for locals.
* Be consistent.
* Use active names for functions.
* Be accurate.
* Indent to show structure.
* Use the natural form for expression.
* Parenthesize to resolve ambiguity.
* Break up complex expressions.
* Be clear.
* Be careful with side effects.
* Use a consistent indentation and brace style.
* Use idioms for consistency.
* Use else-ifsfor multi-way decisions.
* Avoid function macros.
* Parenthesize the macro body and arguments.
* Give names to magic numbers.
* Define numbers as constants, not macros.
* Use character constants, not integers.
* Use the language to calculate the size of an object.
* Don't belabour the obvious.
* Comment functions and global data.
* Don't comment bad code, rewrite it.
* Clarify, don't confuse.

Interfaces
----------

* Hide implementation details.
* Choose a small orthogonal set of primitives.
* Don't reach behind the user's back.
* Do the same thing the same way everywhere.
* Free a resource in the same layer that allocated it.
* Detect errors at a low level, handle them at a high level.
* Use exceptions only for exceptional situations.

Debugging
---------

* Look for familiar patterns.
* Examine the most recent change.
* Don't make the same mistake twice.
* Debug it now, not later.
* Get a stack trace.
* Read before typing.
* Explain your code to someone else.
* Make the bug reproducible.
* Divide and conquer.
* Study the numerology of failures.
* Display output to localise your search.
* Write self-checking code.
* Write a log file.
* Draw a picture.
* Use tools.
* Keep records.

Testing
-------

* Test code at its boundaries.
* Tes pre- and post-conditions.
* Use assertions.
* Program defensively.
* Check error returns.
* Test incrementally.
* Test simple parts first.
* Know what output to expect.
* Verify conservation properties.
* Compare independent implementations.
* Measure test coverage.
* Automate regression testing.
* Create self-contained tests.

Performance
-----------

* Automate timing measurements.
* Use a profiler.
* Concentrate on the hot spots.
* Draw a picture.
* Use a better algorithm or data structure.
* Enable compiler optimizations.
* Tune the code.
* Don't optimise what doesn't matter.
* Collect common subexpressions.
* Replace expensive operations by cheap ones.
* Unroll or eliminate loops.
* Cache frequently-used values.
* Write a special-purpose allocator.
* Buffer input and output.
* Handle special cases separately.
* Precompute results.
* Use approximate values.
* Rewrite in a lower-level language.
* Save space by using the smallest possible data type.
* Don't store what you can easily recompute.

Portability
-----------

* Stick to the standard.
* Program in the mainstream.
* Beware of language trouble spots.
* Try several compilers.
* Use standard libraries.
* Use only features available everywhere.
* Avoid conditional compilation.
* Localise system dependencies in separate files.
* Hide system dependencies behind interfaces.
* Use text for data exchange.
* Use a fixed byte order for data exchange.
* Change the name if you change the specification.
* Maintain compatibility with existing programs and data.
* Don't assume ASCII.
* Don't assume English.


.. _The Practice of Programming: https://www.amazon.co.uk/Practice-Programming-Professional-Computing/dp/020161586X
