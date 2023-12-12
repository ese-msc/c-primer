# Pointers - a window to variables
```{index} arrays, pointers
```

## Names, objects and memory addresses

In Python, you are probably familar that different variable names can point to the same object:

_list_example.py_
```python
a = [2]
b = a
b[0] = 1
print(a)
```
Running the above code in the Python interpretter gives the output `[1]`. This is because the names `a` and `b` have both been bound to the same list object, and updating the list via one name updates it via the other. C and C++ allow similar behaviour usuing a concept called "pointer"s. 

A C style pointer holds a location (usually called an address) in your computer's memory, along with an attached data type. This address can be looked up ("dereferenced") to get hold of the underlying value to:
1. use in an expression
2. update via an assignment.


## Syntax and operators

As a C/C++ variable, a pointer must be declared the first time it is used. The syntax for this is

```c
int *a; // This is a pointer to an int
```

When declared this way, `a` holds a memory location (written as a number of a fixed size, usually 64 bits on modern comuputer systems). To actually make it "point" to a "target" we need the memory address of a suitable integer. The language has an operator, `&`, which will get this for us. To dereference (i.e. look up) the value `a` points to, we use the derferencing operator `*`. To assign a new value to the target, we assign it to the dereferenced object, that is `*a`. Let's look at a short C++ program which exercises all this new behaviour

```c++
#include <iostream>

int main(){
    int *a;
    int b = 7; // B is a normal int variable holding the value 7
    a = &b; // point

    std::cout << a << std::endl;; // returns b's memory address.
    std::cout << *a << std::endl; // returns b's value  (i.e. 7).

    *a = 10;                     // updates a's target
    std::cout << b << std::endl; // returns 10
    return 1;
}
```

This embeds a lot of new concepts in one go, so feel free to run this one a few times and check you've got to grips with the new behaviour.

If you think back, we've already seen the `*` operator a few times, and the `&` operator at least once. In particular, `&` is used in C++ to indicate "pass by reference" since it's already the C reference operator. To pass by reference in C we must declare the input arguments as pointers and pass in the *value* of a reference to the object we care about by using the `&` operator.

## Pointers and arrays

Another place the * operator has turned up is when passing 2D arrays into functions. This is because (implicitly) C arrays "decay" into pointers when passed to a function. So this means that both

```c++
/* swap two elements (array version) */
void swap2(int a[]){
    int tmp = a[0];
    a[0] = a[1];
    a[1] = tmp;
}
```
and 
```c++
/* swap two elements (pointer version)*/
void swap2(int *a){
    int tmp = a[0];
    a[0] = a[1];
    a[1] = tmp;
}
```

will work with (essentially) identical behaviour. Related to this, that means the `a[n]` operator works with all pointer variables, and should be interpretted to mean "a dereference of the `n`th block of memory of the size pointed to by `a`).

## Why pointers?

In C, pointers are used of necessity to achieve many techniques like pass-by-reference (i.e. giving values to a function in a way that they can be modified), dynamic memory allocation etc, as well as to avoid copying large objects, both when passing them to functions, and when renaming them.

In C++, pointers are still needed for dynamic memory and form the basis of codes which don't waste time copying memory back and forth, however, the ability to pass references make them less important when interacting with functions.

### Pointers and dynamic memory allocation in C

In the `stdlib` library C introduced functions `malloc` (which allocates a block of memory and returns a pointer to it, without updating any values in the memory) and `calloc` (which allocates and _zeros_ a block of memory and returns a pointer to it) These are roughly equivalent to the `numpy` `empty` and `zeros` functions in Python. Finally the `free` function deallocates the memory to clean up. It's bad practice not to free allocated memory somewhere, but it's up to the programmer to decide where.

Let's write some C code

```c++

#include <stdio.h>
#include <stdlib.h>
int main( ) {

   int n, i;
   int *vals;

   printf( "Enter a number of squares :");
   // Now you know we pass the address of n into scanf
   scanf("%d", &n);

   printf( "\nYou entered: %d\n ", n);

   /* we have to _cast_ the void pointer from malloc
      to the relevant type. */

   vals = (int*) malloc(n * sizeof(int)) ;

   for (i=0; i<n; i++) {
       vals[i] = (i+1)*(i+1);
   }

   // We'll just print the values for now

   for (i=0; i<n; i++) {
       printf("%d\n", vals[i]);
   }

   // clean up
   free(vals);

   return 0;
}
```

### Pointers and dynamic memory allocation in C++

This interface isn't particularly clear or understandable. C++ introduces an alternative method using the keywords `new` and `delete`. Where `malloc` etc take a number indicating the number of bytes, `new` takes a data type and works out the rest for itself. To allocate an array we use a syntax of the form `new int[10]`, which *must* then be deallocated with `delete[]`.

Let's use the C++ approach for our code above:

```c++
#include <iostream>

int main( ) {

   int n;
   int *vals;

   std::cout << "Enter a number of squares :";
   // Now you know we pass the address of n into scanf
   std::cin >> n;

   std::cout << "\nYou entered:" << n <<"\n";

   /* we have to _cast_ the void pointer from malloc
      to the relevant type. */

   vals = new int[n] ;

   for (int i=0; i<n; i++) {
       vals[i] = (i+1)*(i+1);
   }

   // We'll just print the values for now

   for (int i=0; i<n; i++) {
       std::cout << vals[i] <<"\n";
   }

   //cleanup

    delete[] vals;

   return 0;
}
```

We didn't need any extra libraries this time, since `new` and `delete` are baked into the language.


### Additional pointer types

 In C++, traditional pointers are now considered less useful and alternative constructs such as "smart pointers" (which clean themselves up when they pass out of scope) and unique pointers (which prevent multiple pointers all being directed at the same target) are in greater use. You will learn more about these techniques during the rest of the course.

## Summary

We've now had a brief introduction to the concept of pointers, their use and why a programmer might choose to use them in the first place. In the next lesson, we will look at an introduction to creating our own data structures using `struct`s and `class`es.
