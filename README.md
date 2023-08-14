# Build systems

Yet another important tool for development is a build system. A build system takes care of compiling
the source code of a program to generate executables, libraries, or sometimes entire system images.
If you have a single source file, you probably do not need a build system to compile it. However,
modern software often has countless source files with complex dependencies, and a build system is
necessary to manage them altogether. The most basic problem of compiling many source files with
dependencies is that of *recompiling*---often times, you change a small portion of a single file and
you want to recompile your code so you can test the change. Ideally, you should be able to only
recompile the source files that are impacted by your change, i.e., you shouldn't have to recompile
all the other files that your change doesn't really impact at all. Build systems take care of this
basic problem. Of course, they do much more than that, as you will find out.

In this assignment, you will learn the basics of the two of the most popular build systems for C,
Make and CMake. [Make](https://www.gnu.org/software/make/) is a popular build system that has a
[long history](https://en.wikipedia.org/wiki/Make_(software)) from the early UNIX days. Despite the
fact that it's been around for decades, it still remains a popular choice as a build system.
[CMake](https://cmake.org/) stands for *C*ross-platform *Make* and is another popular build system.
As the name suggests, it aims to be cross-platform, meaning that it allows you to use a single CMake
configuration to compile across different platforms. Both Make and CMake have many features but you
will learn just the basics so you can use them in future assignments.

## Task 0: Make

This [Makefile Tutorial](https://makefiletutorial.com/) is a very well-written tutorial that is easy
to follow. As always, you need to record what you do as you follow the tutorial. Here are the
important points for grading.

* Make sure you record what you do with `script -a`.
* Create a directory named `make` and do everything in that directory.
* As the tutorial explains, Makefiles requires tabs. However, we have replaced a tab with two spaces
  in our Neovim setup. In order to enter an actual tab, you need to enter `<Ctrl>-v` first, and then
  a tab.
* You need to do the tutorial up to the section named `Fancy Rules`.
* The tutorial demonstrates various ways to write Makefiles. Your task is to write the Makefiles as
  the tutorial describes and run them to understand how they behave. Since you can create only one
  Makefile per directory, you need to create a separate directory whenever you need to create a new
  Makefile. The directory should be named after the (sub)-section name. Below are the directories
  you need to create. In each of these directories, you need to have a Makefile that contains what
  the tutorial demonstrates in the corresponding section. If the tutorial shows you multiple boxes
  (colored in black) within a section, just include them all in a single Makefile. There are
  exceptions to this as we explain below.
  * `running-the-examples`
  * `the-essence-of-make` (just to make sure you understand the directives from above, Makefile here
    should contain two targets, `hello` and `blah`)
  * `more-quick-examples`
  * `make-clean`
  * `variables` (there are two `all` targets here, so rename them as `all1` and `all2`.)
  * `the-all-target`
  * `multiple-targets`
  * `wildcard1` (the actual section name is `* Wildcard`)
  * `wildcard2` (the actual section name is `% Wildcard`)
  * `automatic-variables`
  * `implicit-rules`
  * `static-pattern-rules` (Makefile here should do the efficient way.)
  * `static-pattern-fules-and-filter`
  * `pattern-rules` (you just need to do the first example.)
  * `double-colon-rules`

## Task 1: CMake

CMake is a "meta" build system in the sense that it generates build files for another build system
(e.g., Makefiles for make) and relies on that build system for actual compilation. What you do with
CMake as a developer is to write configuration files (called CMake scripts) so that CMake can
generate build files. In this task, you will get a sense of how to use CMake. We combine a few
tutorials on the Internet for this task such as [How to Use
CMake](https://earthly.dev/blog/using-cmake/), [Introduction to CMake by
Example](http://derekmolloy.ie/hello-world-introductions-to-cmake/), and [CMake
Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html).

* Make sure you record what you do with `script -a`.
* Create a directory named `cmake` and do everything below in that directory.
* Create a directory named `src` and in it, create two files `main.c` and `add.c`.
* Write the following code in `main.c`.
  ```c
  #include <stdio.h>

  int add(int x, int y);

  int main()
  {
    printf("Adding 2 and 9 together gives you: %d\n" , add(2, 9));
    return 0;
  }
  ```
* Write the following code in `add.c`.
  ```c
  int add(int x, int y)
  {
    return x + y;
  }
  ```
* Compile the code with Clang and see if it works correctly.
* Now, you will use CMake to compile this code. In order to do this, you need a file named
  `CMakeLists.txt`. This is the main configuration file for CMake, and without this, you can't use
  CMake. This file needs to exist in the root directory of your source. So in our example, don't
  create it in `src/`.
* At the minimum, you need to have three commands in CMake, `cmake_minimum_required()`, `project()`,
  and `add_executable()`. `cmake_minimum_required()` specifies the lowest version of CMake that you
  are supporting. `project()` defines a few pieces of information regarding your program.
  `add_executable()` tells CMake the executable name you want to generate and which source files
  CMake needs to use.
* [The syntax for
  `cmake_minimum_required()`](https://cmake.org/cmake/help/latest/command/cmake_minimum_required.html#command:cmake_minimum_required)
  is `cmake_minimum_required(VERSION <min>)` where `<min>` is the minimum version number. For
  example, `cmake_minimum_required(VERSION 3.22)`.
* [The syntax for
  `project()`](https://cmake.org/cmake/help/latest/command/project.html#command:project) is more
  complex, but at least you need to have `project(<project name>)` where `<project name>` is the
  name of your project. You typically want to have more information than that, such as a version
  number, a description, and the language you use. For example, `project(CMakeTutorial VERSION 1.0
  DESCRIPTION "A CMake Tutorial" LANGUAGES C)` contains a project name (`CMakeTutorial`), a version
  number (`1.0`), a description (`"A CMake Tutorial"`), and a supported language (`C`).
* [The syntax for
  `add_executable()`](https://cmake.org/cmake/help/latest/command/add_executable.html#command:add_executable)
  is simple in that you first need to provide the executable name, followed by a list of source
  files. For example, `add_executable(add src/main.c src/add.c)` will generate `add` from
  `src/main.c` and `src/add.c`.
* Edit `CMakeLists.txt` and include the above three commands appropriately for compiling
  `src/main.c` and `src/add.c` and generating `add`.
* Once you have your `CMakeLists.txt`, you can compile your source with CMake. The most standard way
  of doing this is to create a directory called `build` and let CMake generate build files (e.g.,
  Makefiles) and other files under that directory. The reason why you want to do this is to cleanly
  separate your source from build files. To accomplish this, you can enter the following commands
  from your source's root directory. (`$` indicates a shell prompt, so you shouldn't type it when
  you try the commands.)
  ```bash
  $ mkdir build
  $ cd build
  $ cmake ..
  $ make
  ```
  As you can see, you still need to use `make` to compile your source. As mentioned earlier, this is
  because CMake is a "meta" build system.
* Since using a separate `build/` is what everybody does, CMake provides shortcuts. The above
  commands can be replaced with the following.
  ```bash
  $ cmake -S . -B build     # This generates build files in `build/`.
  $ cmake --build build     # This compiles the source and generates an executable.
  ```
  In the above commands, `-S <dir>` tells CMake that `<dir>` is the root of the source. `-B <dir>`
  tells CMake that we want to use `<dir>` for build files. `--build <dir>` tells CMake that we want
  to compile the source using the build files in `<dir>`. 
* Check `build/` and see if CMake has generated `add`, the executable. Run it and make sure it runs
  correctly.
* Now, remove `build/` and everything in it for the next steps.
* Remove `int add(int x, int y);` in `main.c` and create a separate header file named `add.h`
  that contains the line. Create a new directory `include` and put `add.h` in the directory. Edit
  `main.c` appropriately to include the header.
* The source code structure should be as follows.
  ```bash
  .
  |-- CMakeLists.txt
  |-- build
  |-- include
  |   \-- add.h
  \-- src
      |-- add.c
      \-- main.c
  ```
  In fact, this is how developers typically organize a C/C++ source code base---a `CMakeLists.txt`
  in the root directory, a `build/` directory for build files and compiler artifacts, an `include/`
  directory for header files, and a `src/` directory for source files.
* There are two important commands to introduce here to deal with such a source structure. One is
  `include_directories(<dirs>)` that tells CMake where to find header files. For example,
  `include_directories(include)` tells CMake that `include` is a directory under the directory where
  `CMakeLists.txt` is located and there are header files in it. Include this in your
  `CMakeLists.txt`.
* The other command is `file(GLOB <variable name> <wildcard expression>)` that allows us to use a
  wildcard expression to get a list of files and store it in a variable. For example, `file(GLOB
  SOURCES "src/*.c")` will make a list of all `.c` files under `src/` and store the list to a
  variable named `SOURCES`. You can use this variable instead of manually listing out every `.c`
  file under `src/` in `add_executable()`. The only catch here is that when you use a variable in
  `CMakeLists.txt`, you need to use the format of `${<variable name>}`. Thus, you can change your
  `add_executable()` to `add_executable(add ${SOURCES})`. Modify your `CMakeLists.txt` to include
  this new `add_executable()` and the above `file(GLOB ...)` command.
* Once you're done with this task, stop recording and push all the files to your assignment repo for
  grading.

# Next steps

You need to accept the invite for the next assignment (A6).

* Go to this URL: [https://classroom.github.com/a/PGPiPLGw](https://classroom.github.com/a/PGPiPLGw)
* Accept the invite for Assignment 6 (A6).
* If you are not in `units/02-tools` directory, go to that directory.
* Clone the assignment repo.
