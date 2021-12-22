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

A C style pointer holds a location (usually called an address) in you computer's memory, along with an attached data type. This address can be looked up ("dereferenced") to get hold of the underlying value to:
1. use in an expression
2. update via an assignment.


## Syntax and operators

As a C/C++ variable, a pointer must be declared the first time it is used. The syntax for this is
```c++
int *a; \\ This is a pointer to an int
```
When declared this way, `a` holds a memory location (written as a number of a fixed size, usually 64 bits on modern comuputer systems). To actually make it "point" to a "target" we need the memory address of a suitable integer. The language has an operator, `&`, which will get this for us. To dereference (i.e. look up the value) `a` points to, we use the derferencing operator `*`. To assign a new value to the target, we assign it to the dereferenced object, that is `*a`. Let's look at a short C++ program which exercises all this new behaviour

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
return 1
}
```

This embeds a lot of new concepts in one go, so feel free to run this one a few tips and check you've got to grips with the new behaviour.

If you think back, we've already seen the `*` operator a few times, and the `&` operator at least once. In particular, `&` is used in C++ to indicate "pass by reference" since it's already the C reference operator. To pass by reference in C we must declare the input arguments as pointers and pass in the *value* of a reference to the object we care about by using the `&` operator.

## Pointers and arrays

Another place the * operator has turned up is when passing 2D arrays into functions. This is because (implicitly) C arrays "decay" into pointers when passed to a function. So this means that both

```c++
/* swap two elements (array version) */
int[2] swap2(int a[]){
    out[2];
    out[0] = a[1];
    out[1] = a[0] ;
    return out;
}
```
and 
```c++
/* swap two elements (pointer version)*/
int[2] swap2(int *a){
    out[2];
    out[0] = a[1];
    out[1] = a[0] ;
    return out;
}
```

will work with (essentially) identical behaviour. Related to this, that means the `a[n]` operator works with all pointer variables, and should be interpretted to mean "a dereference of the `n`th block of memory of the size pointed to by `a`).

## Why pointers?

## Summary




## Exercises

