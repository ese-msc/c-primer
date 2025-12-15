# Compiling & Running C++ Code
```{index} compiling
```

Whereas Python is mostly fairly simple to get working with straight away, especially when working in interactive mode in a terminal interpreter session or a Jupyter notebook, C & C++ have a few extra hurdles before you can get the computer to run your code. Your program must be compiled (and sometimes linked to other external standard or third party libraries) to produce a separate executable file containing native machine instructions for your system, before that file can be run to finaly solve your problem. In this section we present a number of ways of approaching this, listed in order of ease of use.

## Web based solutions
```{index} compiling:web-based 
```

There are a variety of platforms which will allow you to run small one file C & C++ programs or code snippets directly from your browser. A (non-exhaustive) list of examples includes:
- [Replit](https://replit.com/languages/cpp)
- [Codepad](https://codepad.app/)
- [Ideone](https://ideone.com/)

![](images/replit.jpeg)

On each of these platforms you can cut & paste code from the examples in this primer, and then run the code to generate output, usually with a single click of the mouse on the button labelled `Run`. Note that not all platforms will let you interact with your code while it runs (Replit will, as well as linking to your GitHub account if you'd like to save your work).

## Compiling natively
A more long-term solution, and what you will be using during the Advanced Programming module, is to use a local compiler on your computer. There are many options out there, which depend on which operating system you are using. The following are some popular options available to you.

```{important} In the **Advanced Programming** module in 2025-26, we will be using the following IDE and compiler combination: 
- VS Code
- `gcc` version 15
Please see below for how to install this combination on the relevant operating system for your laptop.
```

### Apple Macs: `gcc` or `clang`
```{index} compiling:mac
``` 

Mac users have a number of routes to set up their system for C++. We recommend the first method (i.e gcc) given below, since it provides most scope to expand later, but for completeness we also document the route to install the Apple C compilers and work with homebrew.

#### gcc, homebrew and VS code

The open source third-party mac package manager [Homebrew](https://brew.sh/) provides preconfigured versions of a number of unix-like packages, including versions of the GNU C/C++ compilers.

Most Mac users on the course will already have Homebrew installed, but for those that don't, the application itself can be downloaded using the script & instructions from the Homebrew homepage. Additional (and alternative) instructions can be found [here](https://docs.brew.sh/Installation). Once this installation is complete, running the command:

```
brew install gcc
```

will install a recent version of `gcc` (version 15 as of early December 2025) as well as placing it in your standard path. Once installed, (and having opened a new terminal) you can confirm that things work by running the following command in a terminal

```
gcc-15 --version
```

You should see a response something like

```
gcc-15 (Homebrew GCC 15.2.0) 15.2.0
Copyright (C) 2025 Free Software Foundation, Inc.
This is free software; see the source for copying conditions. There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

To compile a C++ file called `hello.cpp` into an exectuable called `hello`, then run it, use a command like

```
g++-15 -o hello hello.cpp
./hello
```

Here `g++-15` is the name of your new GNU C++ compiler (specifically, version number 14), the `-o` option specifies the name of the output file (the default is `a.out`) and we must list the `.cpp` source file to compile into it. The second line then runs our new executable file which we have just compiled.

Remember, we only need to compile once, and then we can run the executable as many times as we like. If we make any changes to the source code, we must recompile before we can run the new version and see the results.

#### Xcode

An alternative is to install the [Xcode command line tools](https://mac.install.guide/commandlinetools/4.html) by following the instructions on the linked page (if you haven't already). This gives you access to the Apple version of the clang compiler. 

you can confirm that things work by running the following command in a terminal

```
cc --version
```

You should see a response something like

```
Apple clang version 17.0.0 (clang-1700.4.4.1)
Target: arm64-apple-darwin24.6.0
Thread model: posix
InstalledDir: /Library/Developer/CommandLineTools/usr/bin
```
although the precise values may be a little different.

To compile a C++ file called `hello.cpp` into an exectuable called `hello`, then run it, use a command like

```
c++ -o hello hello.cpp
./hello
```

Here `c++` is the name of your C++ compiler, the `-o` option specifies the name of the output file (the default is `a.out`) and we must list the `.cpp` source file to compile into it. The second line then runs our new executable.


### Linux/WSL: `gcc` or `clang`
```{index} compiling:linux
```

Linux users are likely to find C compilers are either installed by default on most desktop distributions, or readily installable via the system package manager. Given the wide range of distributions in use, we can't hope to cover all of them, but for some of the more popular ones:

- On Ubuntu/Debian (including WSL), use `sudo apt install build-essential`
- On Arch Linux, use `sudo pacman -S gcc`
- On Red Hat/Fedora use `sudo yum install devtoolset-8`
 
Once installed,  you can confirm that things work by running the following command in a terminal:

```
gcc --version
```

You should see a response something like

```
gcc (Ubuntu 13.3.0-6ubuntu2~24.04) 13.3.0
Copyright (C) 2023 Free Software Foundation, Inc.
This is free software; see the source for copying conditions. There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

To compile a C++ file called `hello.cpp` into an exectuable called `hello`, then run it, use a command like

```
g++ -o hello hello.cpp
./hello
```

Here `g++` is the name of your new GNU C++ compiler, the `-o` option specifies the name of the output file (the default is `a.out`) and we must list the `.cpp` source file to compile into it. The second line then runs our new executable.


### Windows: Visual Studio
```{index} compiling:windows native
```

For Windows users only, you can also obtain the Microsoft C/C++ compiler (MSVC) by downloading the Visual Studio community package [here](https://visualstudio.microsoft.com/vs/community/). Visual Studio is a sister package to Visual Studio Code, which combines build tools for several programming languages along with an Integrating Development Environment (IDE) to code them in.

To compile a file, we must create a matching Visual Studio solution file. For a one line program, the easiest way to do this is to start from the `console application` template project, and modify the default file appropriately. We can then compile and run our source using the `Local Windows Debugger` play button, or  the `Debug>Start Debugging (F5)` menu option.

```{note}
While MSVC and Visual Studio are a powerful combi, we will not be using them much in the Advanced Programming module. For those of you who go on to study Patterns for Parallel Programming (ACSE), you will likely see this IDE/compiler combination in more detail.
```

## Summary

You should now have found a method to compile C/C++ programs which works for you. It is fine to use either of the first two options for the duration of this primer, but you will find a local compiler much more use during the actual Advanced Programming course.

In the next section we will start using our compiler to actually build some C++ code, as well as identifying more similarities and differences between C/C++ and Python.

