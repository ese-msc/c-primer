# A "Hello World!" program

## Preface

A common first program for people to code in a new programming language is to write just enough code to print the phrase "Hello World!" to the screen (or other output device) and then exit.

The popularity of this tradition actually dates back to the beginnings of the C programming language in 1978 and the book "The C Programming Language" by Brian Kernighan and Dennis Ritchie.

Let's compare some simple implementations in Python, C and C++.

## Hello World in Python

By now, you should all know enough about Python scripts that you can write a quick implementation of the "Hello World!" program. This will probably look something like the following:

    _hello.py_
    ```python
    print("Hello world!")
    ```
Here we use the builtin Python print function to print to screen, and can either write `"Hello World!"` or `'Hello World!'` to create our string to print.     

## Hello World in C

A C based hello world function might look something like the following:

    _hello.c_
    ```c
    #include <stdio.h>

    int main(void) {
        printf("Hello World!\n");
        return 0;
    }
    ```

Unlike Python, we need to use a function from outside the core language (in this case the function `printf` from the standard library `stdio` ) to print our message to screen. At the compilation stage we do this with command `#include` (a C preprocessor directive), which works somewhat similarly to the `import` statement in Python.

Where Python runs through commands beginning at the top of a script file, in `C` programs (at least, those printing to screen in the terminal) start at the beginning of the special `main` function. This function usually returns an integer, where `0` is taken to mean that things worked successfully, while other values are taken as a sign that something went wrong. 

Finally, in C we **must** use the double quotes `"` to indicate a string, and since the `printf` function doesn't end lines automatically, we must do it ourselves using the special `\n` character.

## Hello World in C++

A C++ based hello world function might look something like the following:

    _hello.cpp_
    ```cpp
    #include <iostream>

    int main() {
        std::cout << "Hello World!" << std::endl;
        return 0;
    }
    ```

You'll see that in this case, the code looks very similar to the C example. In fact, most C code is valid C++ code (possibly with a few small changes). The only thing that looks different is that rather than using a function like `printf` we are using the special `<<` operator (i.e. a token like `+` or `/`) to send our message to `std::cout`, an "output stream" which represents the screen.

## Exercise: Run the Hello World programs

Run the three different programs in Python, C and C++. You already know how to run Python scripts. You can look back to the introduction pages to see how to run C & C++ codes.

Once you can run the programs, try changing the message:
- What happens if you leave out the `\n` instruction in the C example?
- Can you add a second line?

