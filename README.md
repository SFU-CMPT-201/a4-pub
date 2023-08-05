# Build systems

Along with an editor, another important tool for development is a build system. A build system takes
care of compiling the source code of a program to generate executables, libraries, or sometimes
entire system images. If you have a single source file, you probably do not need a build system to
compile it. However, modern software often has countless source files with complex dependencies, and
a build system is necessary to manage them altogether. The most basic problem of compiling many
source files with dependencies is that of *recompiling*---often times, you change a small portion of
a single file and you want to recompile your code so you can test the change. Ideally, you should be
able to only recompile the source files that are impacted by your change, i.e., you shouldn't have
to recompile all the other files that your change doesn't really impact at all. Build systems take
care of this basic problem. Of course, they do much more as you will find out.

The language we use for this course is C, and in this assignment, you will learn the basics of the
two of the most popular build systems for C, Make and CMake. These systems have many features but
you will learn just the basics so you can use them in future assignments. But before looking at
those build systems, let's first look at how an executable is generated from source files.

## Compiler, linker, shared libraries, and static libraries

Conventionally, when we say we "compile" C code, we understand it to mean generating executables
from source files. However, strictly speaking, this is not correct because there are multiple steps
involved and compilation is one of the steps. These are the actual steps: *preprocessing*,
*compiling*, and *linking*.

* Preprocessing: This is the first step of generating an executable and the *preprocessor* looks at
  the source code and transforms it for compilation. Generally, this involves two things. First, it
  removes all comments (`/* */`, `//`, etc.) as those are not going to be compiled. Second, it
  processes all *preprocessing directives*, which are the statements that start with `#` in C (e.g.,
  `#include`, `#define`, etc.). The preprocessor looks at these and transforms them appropriately
  according to their purposes. E.g., for `#include <stdio.h>`, the preprocessor replaces the
  statement with the content of a file named `<stdio.h>`. For `#define NUM 10`, the preprocessor
  replaces all occurrences of `NUM` with `10` in the code.
* Compiling: Once preprocessing is done, the *compiler* transforms C code into machine code. This is
  done by reading a single source file (a `.c` file) and transforming the code into machine-specific
  instructions. These machine-specific instructions are what a CPU can directly execute. The
  compiler stores these instructions in an *object* file that typically has the extension of `.o`.
  For each `.c` (source) file, the compiler generates a corresponding `.o` (object) file. (We note
  that sometimes there is an intermediate step called the *assembly* step is involved, which we do
  not discuss here.)
* Linking: This is the final step of generating an executable. In the most basic form, the *linker*
  takes all `.o` files (if there are multiple `.c` files in the source, which is often the case) and
  combine them to generate a single executable.

## Make exercise

## CMake exercise

# Next steps

You need to accept the invite for the next assignment (A4).

* Go to this URL: [https://classroom.github.com/a/PGPiPLGw](https://classroom.github.com/a/PGPiPLGw)
* Accept the invite for Assignment 4 (A4).
* If you are not in `units/02-tools` directory, go to that directory.
* Clone the assignment repo.
