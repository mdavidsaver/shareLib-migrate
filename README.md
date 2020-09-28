Migrating from shareLib.h to \*_API macros
==========================================

The `convertAPI` script is meant to help in migrating
[EPICS](https://epics-controls.org/) related code using
the `shareLib.h` (aka. `epicsShare*`) method of dllimport/export.

The `convertAPI` script is meant to be run in a source directory
from which a certain (shared) library will be built.

This requires choosing both a header file name, and an
API macro name.  It is recommended to base these on
the name of the shared library they are associated with.
eg. for `mine.dll` or `libmine.so`, choose `mineAPI.h` and `MINE_API`.

For example,

```sh
$ cd mineApp/src
$ convertAPI mineAPI.h MINE_API *.c *.h
### Add near top of Makefile
USR_CPPFLAGS += -DBUILDING_MINE_API
### Install generated header iff other headers are installed containing MINE_API
INC += mineAPI.h

```

This will create the file `mineAPI.h` and __modify__ any `*.c *.h` files
to replace the common usages of the `epicsShare*` macros with the new `MINE_API`.

It will also print some lines to be added to the assoicated Makefile.
