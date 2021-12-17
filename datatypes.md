# Data Types

```{index} datatypes
```

## The basic data types

Just as in `numpy`, C-like languages have data types for variables containing different sorts of data. The standard data types available "out-of-the-box" are: 

- `char` for ASCII characters/single bytes.
- `int` (and friends `short` and `long`) for integers.
- `float` for lower precision floating point numbers
- `double` for higher precision floating point numbers
- `void` for "nothing in particular" data.

## Modifiers, qualifiers specifiers

By prepending additional keywords, the behaviour of data types can be changed in various ways to represent additional data.

The core modifiers are:
    - `signed` indicates integral (i.e `int`, `char` and friends) data types are signed, i.e. take both positive and negative values. This is the default behaviour.
    - `unsigned`indicates integral (i.e `int`, `char` and friends) data types are unsigned, i.e. zero or positive only. Can be useful for counters in big problems.
    - `short` used to indicate a "small" integer value (normally 16 bit). Can be used as `short int a=4;` or just `short a=4;`
    - `long` used to indicate a "large" value, (normally 64 bit for ints or 80 bit floating point). Can be used as `long int a=12345678901234;`, just `long a=12345678901234;`, or as `long double a=1.0e400` (the last isn't used so often).
    - `long long` used to indicate a "very large" integer value.

The core qualifiers are:

- `const` to declare that the underlying data will not change during its lifetime. Used together with a datatype (which might have a modifier attached).
- `volatile` to declare that the underlying data might change at very short notice.

The core specifiers are:
- `register`
- `extern`

## Scope, declarations, definitions & initialization 

Where Python lets its objects switch between types, C-like languages make programmers state the type of a variable name when first used. This type which cannot be changed as long as that variable is accessible by that name. The limits of accessibility of a variable is sometimes called its "scope", and is frequently defined as the narrowest `{  }` block the variable is exposed in (which operates something like the whitespace blocks in Python). This means that code like

```c++
int main() {
    short a=4;
    double a = 6.0;
    return 0;
}
```
and
```c++
int main() {
    {short a=4;}
    a = 6;
    return 0;
}
```
both fail to compile. The first because `a` has been redeclared and the second because the `a` in `a=6;` hasn't been declared to have any type in its own score. Meanwhile

```c++
int main() {
    short a=4;
    {a = 6;}
    return 0;
}
```
and
```c++
int main() {
    {short a=4;}
    double a = 6.0;
    return 0;
}
```
both work fine. Slightly more surprisingly, so will
```c++
int main() {
    short a=4;
    {double a = 6.0;}
    return 0;
}
```
since it is permissible (though definitely not advisable) to declare variables anew in a new block.

## Type conversion

C-like languages have a number of inbuilt rules which they use to convert values from one type to another. Typically they are converted into whatever type has the larger range, and the expression is then evaluated in that type. This means that code such as

```c++
int a = 27;
double b = a*6.0;
```
is permissible, and will probably do what you want. If it doesn't, or if in doubt, the programmer can explicitly force type conversion using casting with a `(`_data type_`)` syntax. As an example
```c++
std::cout << 8/3;
```
will print `2` (integer division, equivalent to the Python `//` operator shows the value without remainder), whereas
```c++
std::cout << (double)8/3;
```
will print `2.66667` (or some other variant depending on precision options). Here the cast converts the `8` to `8.0` (in this case exactly, since the value can be represented in floating point), the `3` is implictly converted to a double precision number for the floating division, then the expression calculated.

## type definitions, enumerations, structures and classes

### The `enum` keyword

A special data type greatly used in C, although somewhat less in C++, is the enumeration. This allows the programmer to create, semi-automatically sequences of named integer constants, which can then be used in the code in comparisions, loops and similar places

The syntax is

```
enum Foo { a, b, c = 8, d, e = 1, f, g = c + c };
//a = 0, b = 1, c = 8, d = 9, e = 1, f = 2, g = 10
```
where the comment describes the value assigned. These constants are most useful when the name is descriptive. Let's define a function as an example:


```c++
enum Fruit {apple, orange, plum}

Fruit get_next_fruit(Fruit x){
    if (x == apple) {
        return orange;
    } else if (x == orange) {
        return plum
    } else {
        return apple;
    }
}
```
This makes code somewhat easier to maintain, understand and extend than generating code by hand.

### The `struct` and `class`

These keywords allow programmers to combine basic data types (and in C++, functions) together into unified constucts which are accessible under a single name. We will cover them in more detail in the final part of the primer.

## Arrays

As well as scalar variables, C (& thus C++) supports _arrays_ of variables, which are collections of data all of the same data type, which can each be accessed element by element using a syntax somewhat similar to Python collections.

```c++
int a[10];  // this declares a to be a ten value array of ints

float b[3][3] = {{1.0, 2.0, 3.0}, {4.0, 5.0, 6.0}, {7.0, 8.0, 9.0}};

for (int i=0; i<10; i++) {
  std::cout <<a[i] <<", "; // Access (in this case print) an element
}
std::cout  <<"\n";
for (int i=0; i<3; i++) {
  for (int j=0; j<3; j++) {
  std::cout << b[i][j]<<", ";
  }
  std::cout << "\n";
} 

```

Unlike Python, there are no slice operators and arrays need to be dealt with one by one, and we can't quickly print a whole array just by its name (you'll learn why when we talk about pointers.)

To pass a one dimensional array into a function we must declare it specially

```c++
float mean(float a[], int length){
    float sum = 0;
    for (int i=0; i<length; i++) {
        sum += a[i];
    }
    return sum/length
}
```

Note that in our example we've passed in the length of the C-style array explicitly. It's often hard to calculate this in a program, so this is a common (but annoying) technique. To pass a multidimensional array to a function, we replace the `[]` (other than the last one) with a `*` (which means that we are actually passing in pointers).

```c++
float det_2d(float a*[]){
    return a[0][0]*a[1][1]-a[0][1]*a[1][0] //the 2x2 determinant.
}
```

## The C++ standard library

Since C-style arrays are so limited, C++ introduces additional data types, some of which are near equivalents to those in Python. It also introduces additional frameworks to build new ones from existing types. A simple example is the `vector` type, which behaves something like a Python list (i.e. it is a container which autmomatically expands to fit its input)

```c++
#include <iostream>
#include <vector> // library types need an include

int main() {

std::vector<int> vec ={1,2,3}; //use {} to initialise

std::cout << "How many elements?";
int n;
std::cin >> n;

for (int i=3; i<n; i++) {
    vec.push_back(i*i);// Add a new entry, like Python list.append()
}

for (int i=0; i<n; i++) {
    std::cout << vec[i]<< "\n";; // access is still through []
}
```

A basic comparison table:

|Python |C++|
|:-----:|:-:|
| `str` | `std::string`|
| `list`| `std::vector` |
| `dict`| `std::map` |
| `array`| `std::array` (1d )|


## Summary

We've now seen the basic C++ data types in some detail, along with a swift introduction to other key data structures which will be covered in full during the advanced programming course. In the next section we will cover the key operations which can be performed on these variables.

## Exercises