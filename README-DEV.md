## Patch for missing `<exception>` header

Packaging `immer` revealed an issue on FreeBSD and older Debian versions where `std::terminate()` was not resolved due to a missing `#include <exception>` in `operations.hpp`.

### Details

```
clang++-18 -I/tmp/build/libimmer-0.8.1-a.0.20250215170132.6d9f4d308b98/include -I/tmp/dist/libimmer-0.8.1-a.0.20250215170132.6d9f4d308b98/include -Wall -O3 -std=c++26 -stdlib=libc++ -Wno-unqualified-std-cast-call -finput-charset=UTF-8 -o libimmer-0.8.1-a.0.20250215170132.6d9f4d308b98/tests/basics/driver.o -c -x c++ /tmp/dist/libimmer-0.8.1-a.0.20250215170132.6d9f4d308b98/tests/basics/driver.cpp
In file included from /tmp/dist/libimmer-0.8.1-a.0.20250215170132.6d9f4d308b98/tests/basics/driver.cpp:1:
In file included from /tmp/dist/libimmer-0.8.1-a.0.20250215170132.6d9f4d308b98/include/immer/vector.hpp:11:
In file included from /tmp/dist/libimmer-0.8.1-a.0.20250215170132.6d9f4d308b98/include/immer/detail/rbts/rbtree.hpp:13:
/tmp/dist/libimmer-0.8.1-a.0.20250215170132.6d9f4d308b98/include/immer/detail/rbts/operations.hpp:2206:14: error: no member named 'terminate' in namespace 'std'; did you mean 'template'?
 2206 |         std::terminate();
      |         ~~~~~^~~~~~~~~
      |              template
/tmp/dist/libimmer-0.8.1-a.0.20250215170132.6d9f4d308b98/include/immer/detail/rbts/operations.hpp:2206:23: error: expected unqualified-id
 2206 |         std::terminate();
      |                       ^
```

### Patch details:

```
libimmer/include/immer/detail/rbts/operations.hpp.patch
```

```
--- operations.hpp.orig	2025-02-15 12:10:24.006369117 -0500
+++ operations.hpp	2025-02-15 12:11:25.004542638 -0500
@@ -12,6 +12,7 @@
 #include <memory>
 #include <numeric>
 #include <utility>
+#include <exception>
 
 #include <immer/config.hpp>
 #include <immer/detail/rbts/position.hpp>
```

## Packaging Structure

Decision was made to use `include/` directory with `immer` as a subdirectory. This maintains compatibility with upstream's layout, and does not impact library consumers. That is, it still allow the usual include directive:

```cpp
#include <immer/...>
```

## Notes for future maintenance

- Verify whether the `#include <exception>` issue persists in future `immer` updates.
- Reapply patch file if upstream does not address the missing include (for details, see https://build2.org/build2-toolchain/doc/build2-toolchain-packaging.xhtml#howto-patch-upstream-source).

Update this documentation if further modifications are necessary.
