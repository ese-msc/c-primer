```{index} C Preprocessor
```
# The C preprocessor


This page briefly describes the C preprocessor which is by default run on every file before compilation. The preprocessor modifies the text of the code which is seen by the actual compiler based on its own collection of commands, which are known as preprocessor directives. These commands can add, remove or change code in a number of ways and together act to simplify the process of making code run in multiple configurations or on multiple systems.

## Preprocessor directives.

You have already seen some common preprocessor directives while working with :doc:`header_files`. The `#include` directive is one of the most commonly used and most visible C preprocessor directives, which "under the hood" directs the preprocessor to copy the entire (processed) text of another file into the file being worked on. Similarly, the `#pragma once` or `#if ndef ...` patterns are also directives, either explicitly commanding the preprocesser to only work on the file once, or generating the same effect using a preprocessor variable. The full(ish) list of possible standard directives is

 
| Control Structures | Logging Controls | Others |
|--------------------|---------|-------|
| #if              | #error  | #define |
| #elif| #warning |#pragma|
| #else| | #include|
| #ifdef | | #undef |
| #ifndef | | #line |
| #endif | | |



## Defining preprocessor macros

## Conditionals

Beside `#include`, which appears in many C/C++ files, the conditional directives (i.e. `#if`, `#ifdef`, `#else`, etc.) are often visible. These blocks, terminated by an `#endif` directive, mark out text that is only included if the relevant condition is satisfied. For `#if`, this tests whether the next expression (which must consist of known values, i.e. constants and macro variables, not program variables) evaluates to a positive number. If this is correct, then the text in the block is passed to the compiler. If it isn't, then it's as if the block didn't exist. The `#ifdef` and `#ifndef` respectively test whether the given macro variable exists, or doesn't exist. 

Any if-like block can optionally have an `#else` block attached to if. As with Python or C, the `#else` block matters (i.e. is passed to the compiler) if the first expression doesn't evaluate true, in which case it is compiled. These if blocks can be nested providing every block is terminated correctly.

As a concrete example, consider the following code block:

```c++

#include <iostream>

int main(){

#ifdef __GNUC__
#if __GNUC__ >= 10
    std::cout << "You're using a modern compiler.\n";
#else
    std::cout << "Your compiler is out of support.\n";
#endif
#else
    std::cout << "Not a fan of GCC I see.\n";
#endif

    return 0;
}
```

Depending on the details of the compiler being used this generates three different versions of the program.

On GCC version 10 or newer this is

```c++

#include <iostream>

int main(){
    std::cout << "You're using a modern compiler.\n";
    return 0;
}
```

on older GCC this is

```c++

#include <iostream>

int main(){
    std::cout << "Your compiler is out of support.\n";
    return 0;
}
```

and on other compilers (e.g. clang on Apple or MSVC on Windows) this is 

```c++

#include <iostream>

int main(){
    std::cout << "Not a fan of GCC I see..\n";
    return 0;
}
```

The ability to change the code based on information on the system is useful to support different operating system routines in a single code base.




