# libimmer - Immutable and persistent data structures C++ library

This is a `build2` package for the [`immer`](https://github.com/arximboldi/immer)
C++ library. It provides persistent and immutable data structure.


## Usage

To start using `libimmer` in your project, add the following [`depends`](https://build2.org/bpkg/doc/build2-package-manager-manual.xhtml#manifest-package-depends) value to your [`manifest`](https://build2.org/bpkg/doc/build2-package-manager-manual.xhtml#manifests), adjusting the version constraint as appropriate:


```
depends: libimmer ^0.8.1
```

Then import the library in your `buildfile`:

```
import libs = libimmer%lib{immer}
```


## Importable targets

This package provides the following importable targets:

```
lib{immer}
```

### Importable targets description

* `immer` - Immutable and persistent data structures C++ library.

## Configuration variables

This package provides the following configuration variables:

```
[bool] config.libimmer.no_exceptions ?= false
```

### Configuration variables description

* `no_exceptions` - Whether to build without exception handling support.
