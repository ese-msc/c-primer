# Structures & Classes

### The `struct` keyword (differs between C & C++)

```{index} structs
```

Given the basic data types, an obvious thing to do is to combine them into useful named quantities. For example in the context of a medical record, a person might have a name, an age
and a height. In C++ we can encode all of this into a user defined date type as:

```c++
struct person_t {
    char name[256];
    unsigned int age;
    float height;
}
```
and then use it in the ways we would a basic datatype, e.g. in a function definiton

```c++
#include <string.h> // for strcpy to copy strings

person_t initialize_person(char* name, int age, float heigh){
    person_t person;
    strcpy(person.name, name);
    person.age = age;
    person.height = height;
    return person
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
otherwise, we will need to use `struct person_t` all the time.

You may recognise our `person_t` as behaving a little like a Python class object without any methods. In fact, C++ has classes too, which is one of the places Python got the idea from.

### The `class` keyword (C++ only)

```{index} classes
```

C++ classes share a somewhat similar syntax to C structures, (in fact you can declare them with the `struct` keyword as well) except that:
1. They can mix functions (methods) and data
2. They have a basic system of access controls, defined by the 3 keywords `private`, `protected` and `public`.

A person class might look like:
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

When the `class` keyword is used, the default behaviour is to keep members private (i.e. only allow the class itself to acess them), unless explicitl declared as protected (only the class, derived classes and specially listed classes can acces them) or public (i.e. availble as `x.name` as in Python). We've also declared two class methods, the "constructor", which acts a lot like the a Python `__init__` function, and a "getter" function for the Person's name.

Don't worry too much about the details of classes for now, since you will learn a lot more during the Advanced Programming course.

## Summary

## Exercises