# immer - Postmodern immutable and persistent data structures for C++

This is a [`build2`](https://build2.org/) package repository for [`immer`](https://github.com/arximboldi/immer), a library of persistent and immutable data structures written in C++.

This file contains setup instructions and other details that are more appropriate for development rather than consumption. If you want to use [`immer`](https://github.com/arximboldi/immer) in your [`build2`](https://build2.org/)-based project, then instead see the accompanying [`PACKAGE-README.md`](libimmer/PACKAGE-README.md) file.

The development setup for [`immer`](https://github.com/arximboldi/immer) uses the standard [`bdep`](https://build2.org/bdep/doc/bdep.xhtml)-based workflow.
For example:

```
git clone .../immer.git
cd immer

bdep init -C @gcc cc config.cxx=g++
bdep update
bdep test
```
