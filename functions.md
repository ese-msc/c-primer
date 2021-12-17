# Functions
```{index} functions
```

In this section we will describe in more detail the syntax of C/C++ functions.

## Basic functions

We already have experience of a key C++ function in the `main` routine required as an entry point in every command line program. Remember that the basic syntax was

```c++
int main(int argc, char[]* argv){
    // your code goes here
    return 0;
}
```

This has all the key features of an ordinary C/C++ function. They must have a fixed return type, a name (by which they can be called) and a list of arguments (i.e. a list of variables, along with their own data types). This argument list also counts as the top-level declaration of these variables in the function. The function should ensure that it eventually returns a value of the specified data type (if nothing is to be returned, the function should be declard as `void`).

## Function declarations and definitions
```{index} functions: declaration, functions: definition
```

As we stated above, functions must be declared at first use with data types for the return type and argument list. However, this declaration doesn't actually need to define the function code, which can happen (somewhat) independently.

```c++
\\ a function declaration

int add(int, int)

\\ a declaration and defintion together

int minus(int a, int b){
    return a-b;
}

\\ the function definition for `add`

int add(int a, int b){
    return a-b;
}
```

As you can see, a pure function declaration doesn't do much. The most common use is to define the signature for a function which is actually declared elsewhere. Implicitly this is happening with many `#include` statements, which add necessary function definitions into the current file to allow it to compile.

### Return types
```{index} functions: return types
```

A function can only return one data type, which must be declared along with the function signature. Remember that implicit type conversion rules exist, so if you try to return the wrong type it will sometimes be converted to the type you declared.

```c++
int example(){
    return 3.1; // implicitly converted to integer 3
}
```
## Namespaces
```{index} Namespaces
```



## Class methods

## Optional arguments

## Summary

We've now seen the basics of C++ functions, including how to define (and declare) them, how to call them and some more advanced features. That concludes the work for this section, except for some additional exercises. In the next section, we'll look in some more detail at more advanced features, like pointers, classes and header files.

## Exercises