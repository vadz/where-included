Where-Inc
=========

Simple script to find all files including the given C or C++ header file,
possibly indirectly, via some other header. I.e. unlike a simple `grep -l
'#include "foo.h"' *.h`, `where-inc foo.h *.h` will also find the headers
including `bar.h` which, in turn, includes `foo.h`. This can be useful to find
possible dependencies in a big project.

Installation
------------

This is a Perl script without any non-core dependencies, so it doesn't require
any installation but does require a working Perl (any not horribly outdated
version should do).

Usage
-----

Typically the script will be called with at least some header files, as
otherwise it work in almost the same way as `grep` (except much slower), e.g.

    where-inc foo.h include/*.h src/*.cpp

If it's unclear how some file in the output ends up including the header,
`--show-how` option may be added to display the inclusion path.

It is also possible to show all (input) files _not_ including the given header
using the `--invert-match` option or its short form `-v`:

    where-inc -v prologue.h include/*.h

If the headers being searched are included not just by their name but using
some prefix, e.g. `#include <mylib/foo.hpp>`, then this prefix must be given
on the command line using `--prefix` or `-p`, for short, option for the
correct operation:

    where-inc -p mylib mylib/foo.h include/mylib/*.h

The `--verbose` option can be added to show some informative messages.

Bugs
----

Probably many, but the main limitation is that the script makes no attempt to
parse the input sources, beyond recognizing C and C++ comments in them, so it
still considers the files including the given header inside `#if 0` or similar
as including it.

Licence
-------

MIT, see `LICENSE` file for the details.
