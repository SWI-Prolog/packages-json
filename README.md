# SWI-Prolog JSON package

This package provides `library(json)` and related libraries for managing
JSON documents in SWI-Prolog.

These files used to be part of the  `http` package. They have been moved
to a new package as minimal installations  may want to have JSON support
without  needing  HTTP  support.   This    package   installs   backward
compatibility libraries in the  old   locations.  These libraries merely
load the library  from  the  new   location  and  prints  a _deprecated_
message.
