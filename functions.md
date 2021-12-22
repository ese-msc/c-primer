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

### Function declarations and definitions
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

### Pass by value

C (and C++ by default) uses a calling pattern called "pass by value", in which a new copy of the input variables are created, and set to the evaluated value the calling function passes in. Amoung other things, this means that changes to a scalar variable inside a function don't pass back out

```c++
int function add_three(int a){
    a += 3; // Only changes the local a
    return a
}

int main(){
    a = 7;
    b = add_three(a); // b is now 10, but a is still 7.
}
```

In C++ you can also use "pass by reference", where the calling function uses the same memory location as the object passed in to it:

```c++
int function add_three(int &a){ // Note the & sign
    a += 3; // Now changes the input a
    return a
}

int main(){
    a = 7;
    b = add_three(a); // a and b both now 10.
}
```

C can get the same behaviour using pointers (see the next section), although it's a certain amount of work. Pass by reference is more efficient when using large objects, since it saves initializing and copying to the new variable, however it can make your functions more surprising by changing their inputs without it being obvious.


### Return types
```{index} functions: return types
```

A function can (and _must_) only return one data type, which must be declared along with the function signature. Remember that implicit type conversion rules exist, so if you try to return the wrong type it will sometimes be converted to the type you declared.

```c++
int example(){
    return 3.1; // implicitly converted to integer 3
}
```

If your function really doesn't return anything, then its return type must be set to `void`. C++ (but not C) allows you to use the `auto` keyword so that the compiler will guess the return type for you

```c++
auto ex1(){
    return 3; // returns an int
}

auto ex2(){
    return 3.2; // returns a double
}
```
If you do this, you can still only return one type, which is worked out from the first return in the function.

## Namespaces
```{index} Namespaces
```

You've already seen the concept of namespaces in Python, where the stuff inside an imported module are access as (e.g.) `mymodule.myfunction`. The big advantage in this is that this allows multiple functions to have the same name without interfering with each other. C++ allows something very similar with the `namespace` keyword. This allows defining namespaces in which functions (especially #`include`d functions) live. You've actually already seen this with `std::cout`, which is in the `std` namespace.

To define your own namespaces you can write:

```c++

namespace myfuncs
{
    int a_cool_function(int n){
        int out = 1;
        for (int i=1; i<=n; i++){
            out *= n;
        }
        return out
    }

    // You can add more functions & classes here.
}
```
These are then accessed as `myfuncs::a_cool_function` etc.

Similar to the Python `from mymodule import myfunction`, you can also pull names into your current namespace with the `using` keyword in a line like

```c++
using myfuncs::a_cool_function;

int main(){
    int a = a_cool_funtion(40);
}
```

The equivalent to `from mymodule import *` is `using namespace myfuncs;`. Indeed, many tutorials will have `using namespace std` in them, which shortens I/O calls, etc. As with the Python version, this is probably a bad idea unless you are very clear on what you are doing, since it exposes you to a variety of hard to diagnose bugs.

## Optional arguments and a lack of keywords

As with Python, in C++ functions can be created with optional (for default value) argument variables, with a similar syntax:

```c++
#include <string>
#include <iostream>

void hello(std::string name="Mary"){
    std::cout << "Hello " << name;
}
```

Unlike Python however, C++ does _not_ currently support keyword (a.k.a parameter names) in argment lists. The only way to identify which argument is which is by the order they appear in the calling list.

## Summary

We've now seen the basics of C++ functions, including how to define (and declare) them, how to call them and some more advanced features. That concludes the work for this section, except for some additional exercises. In the next section, we'll look in some more detail at more advanced features, like pointers, classes and header files.

## Exercises