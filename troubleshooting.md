# Debugging & Troubleshooting

## Compiler error messages

Just as with Python, C gives you some useful messages when it can't work out what to do with your code. However, since we are using a compiled language, they appear at compile time rather than when we attempt to run the program. Let's get ourselves a simple example. Suppose we forget to include the `iostream` header in our Hello World example:

_bad_hello.cpp_:
```c++
    int main() {
        std::cout << "Hello World!" << std::endl;
        return 0;
    }
```

GCC gives us the following error messages:

```
bad_hello.cpp: In function 'int main()':
bad_hello.cpp:2:14: error: 'cout' is not a member of 'std'
    2 |         std::cout << "Hello World!" << std::endl;
      |              ^~~~
bad_hello.cpp:1:1: note: 'std::cout' is defined in header '<iostream>'; did you forget to '#include <iostream>'?
  +++ |+#include <iostream>
    1 |     int main() {
bad_hello.cpp:2:45: error: 'endl' is not a member of 'std'
    2 |         std::cout << "Hello World!" << std::endl;
      |                                             ^~~~
bad_hello.cpp:1:1: note: 'std::endl' is defined in header '<ostream>'; did you forget to '#include <ostream>'?
  +++ |+#include <ostream>
    1 |     int main() {
```

For C++ compilers error messages should typically be read from top to bottom, since it's possible that later errors are caused by the first one. In this case, the error message not only identifies the problem, but the solution too! This isn't the common case, in which the compiler will tell you what it doesn't understand, but will be unable to help you. For the record, the Visual Studio Windows compiler gives an example of this sort of less useful message:

```
1>ConsoleApplication3.cpp
1>C:\Users\origi\source\repos\ConsoleApplication3\ConsoleApplication3\ConsoleApplication3.cpp(2,10): error C2039: 'cout': is not a member of 'std'
1>C:\Users\origi\source\repos\ConsoleApplication3\ConsoleApplication3\predefined C++ types (compiler internal)(367): message : see declaration of 'std'
1>C:\Users\origi\source\repos\ConsoleApplication3\ConsoleApplication3\ConsoleApplication3.cpp(2,15): error C2065: 'cout': undeclared identifier
1>C:\Users\origi\source\repos\ConsoleApplication3\ConsoleApplication3\ConsoleApplication3.cpp(2,41): error C2039: 'endl': is not a member of 'std'
1>C:\Users\origi\source\repos\ConsoleApplication3\ConsoleApplication3\predefined C++ types (compiler internal)(367): message : see declaration of 'std'
1>C:\Users\origi\source\repos\ConsoleApplication3\ConsoleApplication3\ConsoleApplication3.cpp(2,45): error C2065: 'endl': undeclared identifier
1>Done building project "ConsoleApplication3.vcxproj" -- FAILED.
```

## Common compiler errors

### Missing punctuation

Probably the most common error for beginners in C/C++ (especially those coming from Python) is to fail to include the `;` symbol to indicate the end of a statement. This means that the compiler will attempt to interpret two lines as if they were one and can produce a surprisingly wide variety of error messages. One of the more typical looks something like

```
In function 'int main()':
Line 5: error: expected ',' or ';' before 'std'
```

which has the advantage of pointing out the fix.

### Undeclared variables

Another very common C/C++ error is to attempt to use a variable name which hasn't been declared to have a specific data type. This can be because you forgot, because you've changed the order of pieces of the code (e.g. ), or because you made a typing error (no pun intended) while entering the name. As a trivial example, consider the following code.

```
int main(){
    int a = 3;
    b = 4;
    a += b;
    return 0;
}
```

On GCC we see this error message

```
no_declaration.cpp: In function 'int main()':
no_declaration.cpp:3:5: error: 'b' was not declared in this scope
    3 |     b = 4;
```

This time, the compiler can't tell us what to do, but we either need to declare the datatype of the variable (in this case, we can change the third line to `int b=4;` _or_, less likely, `double b=4;` as appropriate.) or fix our typing error.

### Incompatible data types

As strongly typed languages, C/C++ only allows inputs to functions if the input datatype is compatible with the function declaration. As an example, consider the following:


```
#include <iostream>

void print_with_endline(char* string){
    std::cout << string << std::endl;
}

int main(){
    int a = 3;
    print_with_endline(a);
    return 0;
}
```

Here we've declared (and defined) a new function, `print_with_endline` which accepts a string (strictly, a pointer to a character which starts a character array, you'll learn more in Part III), but called the function with an integer. This isn't a conversion which is declared by default, since it's ambiguous whether you're likely to want to view the integer as one byte, as a sequence of bytes, or as the string which represents the integer value. The error message from GCC is:

```
bad_datatype.cpp: In function 'int main()':
bad_datatype.cpp:9:24: error: invalid conversion from 'int' to 'char*' [-fpermissive]
    9 |     print_with_endline(a);
      |                        ^
      |                        |
      |                        int
bad_datatype.cpp:3:31: note:   initializing argument 1 of 'void print_with_endline(char*)'
    3 | void print_with_endline(char* string){
      |                         ~~~~~~^~~~~~
```

Again this doesn't tell us what to do, it's up to the programmer to sort out what they intended (e.g. to call another function, to convert the integer to bytes, or to convert it into a string using another function first).

## Compiler non-errors

Although the compiler flags many code mistakes that it can't compile, there are also many mistakes that it won't catch, at least by default. One of the most famous, though not necessarily the most frequent is the class of off-by-one errors when working with arrays and similar containers. As an example:

```c++
#include <iostream>

int main(){
    int a[] = {1,2,3,4,5};
    for (int i=0; i<=5; i++) {// Test should be i<5!
        std::cout << a[i];
    }
    return 0;
}
```

This code will compile (in the absence of additonal compiler options) and run without question, however, after printing the 5 integers in `a` it will then print the next few bytes it finds in the program memory, as if they were an integer.

Other common errors which might still compile include basic coding failings in logic, mathematics as well as mistakes like using a bare array name instead of accessing an element. Ultimately, these are the programmer's responsiblity to test for and catch while writing the code.


## Summary

We've now seen some of the more common error messages our compiler might throw at us, as well as some tips on how to deal with them. In the next section we'll have some more exercises to try to practice writing basic programs, before we move on to a more in-depth look at the workings of a C++ program.
