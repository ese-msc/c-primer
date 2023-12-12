# Header files and libraries
```{index} header files
```

## Working with multiple files

So far, we've always been writing code assuming that everything is is the same "compilation unit" (i.e. in the same file, compiled at the same time). This is fine for small programs, but as the amount of code increases, and as you begin working with other people, it can become very useful to divide your source code into multiple files.

If there is a clear separation between the various components, then this is easy enough to do (the Advanced Programming course will cover some more of the details). However, more usually there will be at least one file which needs to call a function from another file. To do this, the calling file needs to have declarations (i.e. information on the return type and permissible arguments), but not defintions (i.e it doesn't need the actual function code).

We could just type up the declaration afresh every time it is used, but that violates the Don't Repeat Yourself (DRY) programming principle. In particular, if you change the original function in a way which affects the definition, you then need to search out every since file which uses it, rather than changing in one place.

Instead, the standard which has developed is to use the `#include` preprocessor directive to grab one canonical file containing the proper declarations. This file is called a _header file_, using the file extension `.h`, and you have already been using them implicitly in your coding whenever you've used an `#include` line.

### Standard layout

The `#include` directive works by copying the text of the requested file directly into the file being worked on. Since the header file itself might have `#include` lines, this is an iterative process. To avoid infinite loops, or accidentally giving the same declaration twice, modern header files start with

```c++
#pragma once

/*declarations start here*/
```

This tells the compiler to only copy the file in once, even if it sees it multiple times. Older header files achieve the same behaviour using a trick


```c++
#ifndef A_SPECIAL_UNIQUE_STRING
#define A_SPECIAL_UNIQUE_STRING 1

// All the declarations go here

#endif
```

where the unique string is likely to be based on the name of the file, program or package.

## Libraries

To share code for others to use, there are two options in C/C++:
1) share the source files and let the user compile it together themselves
2) Compile it for the users' computer and then share the compiled data for the user to link to.

One version of the first option is called a "headers only" library, in which all the necessary code is contained in `.h` files, which only need to be `#included` to use them. We will see an example of a "headers only" library in the group project in the final week of the Advanced Programming course. The second option is more complicated, especially for C++ code.

This is because different C compiler versions (running on the same operating system and basic hardware) normally produce code which will work with all other C compilers, whereas C++ code is linked much more strongly to the compiler which produced it. This means that you need to find & install a version of the library for your specific compiler version in order to be able to use it.

To link in a compiled library (assuming you've already installed it), additional options must be set for your compiler. On the command line, this often means adding additional search paths (using the `-L` option) and library files to include. We won't try to go into these details now, you will find out more during the course.


## Summary

We've had a brief look at the hows and whys of header files and writing code you can share with others. This concludes the formal part of the C++ primer, beyond some more exercises. If you have further questions (or have spotted any bugs) feel free to ask on Teams. The Advanced Programming team look forward to meeting you in the new year.

## Exercises