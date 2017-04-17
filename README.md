C++ B-tree
==========

C++ B-tree is a template library that implements ordered in-memory containers based on a B-tree data structure.  Similar to the STL map, set, multimap, and multiset templates, this library provides btree\_map, btree\_set, btree\_multimap, and btree\_multiset.

C++ B-tree containers have a few advantages compared with the standard containers, which are typically implemented using Red-Black trees. Nodes in a Red-Black tree require three pointers per entry (plus 1 bit), whereas B-trees on average make use of fewer than one pointer per entry, leading to **significant memory savings**. For example, a `set<int32_t>` has an overhead of 16 bytes for every 4 byte set element (on a 32-bit operating system); the corresponding `btree_set<int32_t>` has an overhead of around 1 byte per set element.

B-trees are widely known as data structures for secondary storage, because they keep disk seeks to a minimum. For an in-memory data structure, the same property yields a performance boost by keeping cache-line misses to a minimum. C++ B-tree containers make better use of the cache by performing multiple key-comparisons per node when searching the tree. Although B-tree algorithms are more complex, compared with the Red-Black tree algorithms, the improvement in cache behavior may account for a **significant speedup** in accessing large containers.

The C++ B-tree containers are not without drawbacks, however. Unlike the standard STL containers, modifying a C++ B-tree container **invalidates all outstanding iterators** on that container. For this reason, the library also contains "safe" variations on the four containers: iterators on safe B-tree containers keep a copy of the current key and automatically reposition the iterator whenever it is used.


This fork
---------
This version is based on the original version from Google,
with the patch applied for supporting non-C++11 compilers.

Usage
-----
This library is a C++ template library and, as such, there is no
library to build and install.  Copy the .h files and use them!

See https://github.com/piperchester/cpp-btree/wiki/UsageInstructions
for details.

----

To build and run the provided tests, however, you will need to install
CMake, the Google C++ Test framework, and the Google flags package.

Download and install CMake from http://www.cmake.org

Download and build the GoogleTest framework from
http://code.google.com/p/googletest

Download and install gflags from https://code.google.com/p/gflags

Set `GTEST_ROOT` to the directory where GTEST was built.
Set `GFLAGS_ROOT` to the directory prefix where GFLAGS is installed::

	export GTEST_ROOT=/path/for/gtest-x.y
	export GFLAGS_ROOT=/opt
	cmake . -Dbuild_tests=ON

For example, to build on a Unix system with the clang++ compiler::

	export GTEST_ROOT=$(HOME)/src/googletest
	export GFLAGS_ROOT=/opt
	cmake . -G "Unix Makefiles" -Dbuild_tests=ON -DCMAKE_CXX_COMPILER=clang++

