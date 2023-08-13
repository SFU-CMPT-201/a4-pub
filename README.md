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

## Make

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

## CMake

CMake is a "meta" build system in the sense that it generates build files for another build system
(e.g., Makefiles for make) and relies on that build system for actual compilation. What you do with
CMake as a developer is to write configuration files (called CMake scripts) so that CMake can
generate build files for another build system.

# Next steps

You need to accept the invite for the next assignment (A4).

* Go to this URL: [https://classroom.github.com/a/PGPiPLGw](https://classroom.github.com/a/PGPiPLGw)
* Accept the invite for Assignment 4 (A4).
* If you are not in `units/02-tools` directory, go to that directory.
* Clone the assignment repo.
