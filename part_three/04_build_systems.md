# Build Systems

This section is more advanced, and is not required for the Advanced Programming module.  It is included here for reference, for those who are interested and for those who want to use external libraries in their projects. It may be useful for ACSE students preparing for the Patterns for Parallel Programming module.

## Introduction

When you write a C++ program, you need to compile it.  This is fairly simple when all you have is a single file, but as soon as you start to have multiple files, or want to use external libraries, things get more complicated.  In this section we'll look at some of the options for building C++ programs with external, and how to use them.

This will not go into great detail on the build systems themselves, but will give you enough information to get started with them.  If you want to know more, there are plenty of resources online.

In general there are two steps involved:

1. Making sure the  the path for the header files which contain the declarations for the library are available to the compiler
2. Making sure the path for the library files which contain the compiled code for the library are available to the linker.

How to do this depends on the build system you are using. We will give a short explanation here, or you can look at the following tutorials for more


- [Visual Studio](https://docs.microsoft.com/en-us/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp?view=msvc-160)

- [Make](https://www.cs.colby.edu/maxwell/courses/tutorials/maketutor/)
- [CMake](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)

## Visual Studio (Windows only)

Since Visual Studio is mostly used via its graphical interface, it can be hard to find the settings you need to change.  The following instructions should help you to get started.

### Adding header files

Assuming you have already downloaded the external library you want to use, you will need to know the file path to the directory containing the header  (i.e the `.h` or `.hpp` files).

To add a header file to your project, right click on the project name in the Solution Explorer and select `Properties`.  This will open a new window with a list of options on the left.  Select `C/C++` and then `General`.  In the `Additional Include Directories` box, add the path to the directory containing the header files you want to use.  You can add multiple paths by separating them with a `;`, something like `C:\Users\Downloads\path\to\headers;C:\Users\Downloads\path\to\more\headers`.

### Adding library files

Now you will need to find the file path to the directory containing the library files (i.e the `.lib` or `.dll` files) for the library you want to use.

To add a library file to your project, right click on the project name in the Solution Explorer and select `Properties`.  This will open a new window with a list of options on the left.  Select `Linker` and then `General`.  In the `Additional Library Directories` box, add the path to the directory containing the library files you want to use.  You can add again add multiple paths by separating them with a `;`, something like `C:\Users\Downloads\path\to\libraries;C:\Users\Downloads\path\to\more\libraries`.

If the paths are correct, you can then add the name of the library file to the `Additional Dependencies` box.  This should be the name of the library file without the extension.  For example, if you want to use the library `libexample.lib`, you would add `libexample` to the `Additional Dependencies` box.

You should now be able to use the library in your project and compile it as normal.

## Make (Linux/WSL and Mac only)

The Make build system is used on Linux and Mac.  It is a command line tool, so you will need to open a terminal to use it (and may need to install it if it is not already installed).

On Ubuntu, you can install it with:

```bash
sudo apt install make
```

On Mac, you can install it with:

```bash
brew install make
```

To use Make, you need to create a `Makefile` in the same directory as your source code.  This file contains instructions for how to build the various steps of your program. The following is a simple example of a `Makefile` for a program called `hello`, assuming that the source code is in a file called `hello.cpp`, and your compiler is `g++`:


```makefile
all: hello

CXX = g++

hello: hello.o
    ${CXX} -L/usr/lib/x86_64-linux-gnu/ -lgraphviz -o hello hello.o

hello.o: hello.cpp
    ${CXX} -I/usr/include/graphviz -c hello.cpp
```

The first line defines a target called `all`.  As the first entry, this is the default target, so if you run `make` without specifying a target, it will run the `all` target.  The `all` target depends on the `hello` target, so running `make all` will run the `hello` target.

The `hello` target depends on the `hello.o` target, so running `make hello` will run the `hello.o` target (if `hello.cpp` is newer than `hello.o`), and then the `hello` target.

### Adding header files

The `hello.o` target tells `make` how to compile the `hello.cpp` file into an object file.  The `-I` flag tells the compiler where to look for  header files which weren't installed to system directories.  In this case, the header files are in `/usr/include/graphviz`.

### Adding library files

The `hello` target tells `make` how to link the `hello.o` object file into an executable.  The `-L` flag tells the linker where to look for library files which weren't installed to system directories.  In this case, the library files are in `/usr/lib/x86_64-linux-gnu/`.  The `-l` flag tells the linker which library to use.  In this case, the library is called `libgraphviz.so`, so the flag is `-lgraphviz` (note that the `lib` prefix and the `.so` suffix are omitted).

## CMake (Linux, Mac and Windows)

CMake is a cross-platform build system.  It is a command line tool, so you will need to open a terminal to use it (and may need to install it if it is not already installed).

The biggest issue with both Visual Studio and `make` is that we need to find the header/library files ourselves before we can use them.  CMake can help with this, as it can find the header/library files for us.

Further, `CMake` works fully cross-platform, so the same setup (described as text in a `CMakeLists.txt` file) will work on Windows, Linux and Mac.

### installing CMake

On Ubuntu, you can install it with:

```bash
sudo apt install cmake
```

On Mac, you can install it with:

```bash
brew install cmake
```

### An example CMakeLists.txt file


```cmake

cmake_minimum_required(VERSION 3.10)

project(hello)

set(CMAKE_CXX_STANDARD 17)

find_package(graphviz REQUIRED)

add_executable(hello hello.cpp)

target_link_libraries(hello PRIVATE graphviz)
```



