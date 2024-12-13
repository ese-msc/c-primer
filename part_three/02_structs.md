# Structures & Classes

### The `struct` keyword (differs between C & C++)

```{index} structs
```

Given the basic data types, an obvious thing to do is to combine them into useful named quantities. For example in the context of a medical record, a person might have a name, an age
and a height. In C++ we can encode all of this into a user defined data type as:

```c++
struct person_t {
    char name[256];
    unsigned int age;
    float height;
}
```
and then use it in most of the ways we would a basic datatype, e.g. in a function definiton

```c++
#include <string.h> // for strcpy to copy strings into memory

person_t initialize_person(char* name, int age, float height){
    person_t person;
    strcpy(person.name, name);
    person.age = age;
    person.height = height;
    return person
}

int compare_height(person_t &person1, person_t &person2){
    /* Compare heights of two person_t data structures.
    
    Some people don't like having functions
    with multiple return statements. This could also
    use a variable */
    if (person1.height > person2.height){
        return 1; // person 1 is taller
    } else if (person1.height == person2.height) {
        return 0; // heights are equal
    } else {
        return -1; // person 1 is taller
    }
}

```

We can then pass our `Person` datatypes around like any other variable.

To get the same behaviour in C, we must write

```c
typedef struct {
    char name[256];
    unsigned int age;
    float height;
} person_t;
```
otherwise, we would need to use `struct person_t` all the time instead of just `person_t`.

You may recognise our `person_t` as behaving a little like a Python class object without any methods. In fact, C++ has classes too, which is one of the places Python got the idea from, and the main feature which initially differentiated it from ordinary C.

### The `class` keyword (C++ only)

```{index} classes
```

C++ classes share a somewhat similar syntax to C structures, (in fact you can declare them with the `struct` keyword as well, which the compiler treats almost identically) except that:
1. They can mix functions (methods) and data
2. They have a basic system of access controls, defined by the 3 keywords `private`, `protected` and `public`.

A person class in C++ might look like:
``` c++
class Person {
        char name[256];
        unsigned int age;
        float height;
    public:
        Person(char*, int, float);
        get_name() {return name};
}

Person::Person(char* n, int a, float h){
    name = n;
    age = a;
    height=h;
}
```

When the `class` keyword is used, the default behaviour is to keep members private (i.e. only allow the class itself to acess them), unless explicitly declared as protected (only the class, derived classes and specially listed classes can access them) or public (i.e. available as `x.name` like in Python). We've also declared two class methods, the "constructor", which acts a lot like the a Python `__init__` function, and a "getter" function for the `Person`'s name.

You don't need to worry too much about the advanced details of classes for now, since you will learn a lot more over the duration of the Advanced Programming course.

## Summary

We've now seen the basics of creating our own data structures with `struct` to wrap together related data, making it simpler to pass around. We've also seen that C++ classes allow data and functions acting on that data to be encapsulated together. In the next (and last) page of the main Primer we'll talk a little bit about header files, which are the things that the `#include` statements work with, and allow people to share their precompiled code with others.
