========
Keywords
========

C Keywords
##########

Storage keywords
================

.. glossary::

    auto (C version)
        Declare variable which is automatically cleaned up when coming out of scope and is stored locally (i.e. exactly the default behaviour). *C++ behaviour is different*

    register
        *Suggests* to the compiler that the variable should be stored in a register rather than RAM. This allows fast access, but limits behaviour (e.g. it cannot be used with `&`).

    static
        Declare a variable which exists for the lifetime of the program.

    extern
        Declare a variable name which has memory storage assigned elsewhere.

Datatype keywords
=================

.. glossary::

    char
        One byte data type, often used to store text with ASCII encoding.

    const
        Qualifier indicating a variable will not change its value while it is in scope.

    double
        A double precision (i.e. usually 64 bit, 8 byte) floating point number. Directly equivalent to the Python `float` or `numpy` `float64`.

    enum
        Declare a list of names which are mapped to integer values (automatically, if manual values aren't given).

    float
        A single precision (i.e. usually 32 bit, 4 byte) floating point number. Equivalent to the `numpy` `float32`.

    int
        An integer (usually 4 bytes on modern systems). Equivalent to `numpy` `int32`.

    long
        By itself declares a long integer (usually 8 bytes on modern systems). Equivalent to `numpy` `int64`. Can also be used as a qualifier with `double` for 10 byte floating point number.

    restrict
        Qualifier which indicates that a pointer is the only pointer which can access the memory it points to. This allows the compiler to make optimisations which would otherwise be unsafe.
        
    short
        A 2 byte integer. Equivalent to `numpy` `int16`.

    signed
        Qualifiers which declares integers to be signed (i.e take both positive and negative numbers). Default behaviour.

    struct
        Declares a combined data structure containing other datatypes as separate members.  

    typedef
        Declare an alias for a (possibly qualified) datatype.

    union
        Declares a combined data type containing other data types all sharing the same memory.

    unsigned
        Qualifier which declares integers to be unsigned (i.e. positive, ranging from 0 to the largest number which fits in the memory space).

    void
        Data type representing no specific sort of value.

    volatile
        Qualifier indicating that a value is liable to change at any time. Ensures the compiler will execute commands using the variable in the order they are written.

Control keywords
================

.. glossary::

    break
        Exit the innermost loop (in the current scope) currently executing.

    case
        Declare one option in a `switch` statement.

    continue
        Skip to the next iteration of a loop.

    default
        Declare a default option for a `switch` statement.

    do
        Start a `do ... while` loop block.

    else
        Declare alternative behaviour for an `if` block, executed when the `if` statement is not true.

    for
        Declare a `for` loop.

    goto
        Jump to another labelled section of code (Use with great care).

    if
        Declare a conditional code block, which runs only when the test expression is true.

    inline
        Function specfier which *suggests* to a compiler that it places the relevant code directly in place, avoiding the overhead of a function call.

    return
        Exit a function and pass any `return` value (which must be convertable to the specified data type) to the calling routine.

    switch
        Declare a `switch` block with multiple cases.

    while
        Either declare a `while` loop, or terminate a `do .. while` block.

Operator keywords
=================


.. glossary::

    sizeof
        Function-like operator which returns the size (in bytes) of the data type, variable or expression passed in to it.


Other patterns
==============

You also shouldn't use names starting with a double underscore (e.g. `__bad_name`) or a single underscore and a capital letter (e.g. `_Bad_name`).


C++ Keywords
############

C++ has a much longer list of keywords which cannot be used, which includes the C keywords as a subset. See a source such as [C++ reference](https://en.cppreference.com/w/cpp/keyword) for a definitive list. We will just pick out some highlights.

Important keywords
==================

.. glossary::

    auto (C++ version)
        Declare a variable which automatically identifies its data type based on the context in which it is used. *Different from C behaviour*.

    bool
        Boolean datatype.

    catch
        Associate exception handlers with a `try` statement block, somewhat similar to Python.

    class
        Object oriented combined structure holding both data and functions, which usually act upon that data.

    delete
        Delete a variable or object, and return the memory it was using to the operating system.

    false
        Boolean data indicating a false value. Opposite of `true`, and equivalent to `0`.

    friend
        Specifier indicating a function/class can access private or protected data stored in the declaring class.

    operator
        Declares an overloading of an operator for a user declared data type (i.e. lets the programmer use it with standard C++ operators such as `+` or `<<`).

    namespace
        Declare a namespace, which is a way of grouping together related functions and classes (which acts a bit like a Python package/module).

    new
        Allocate new memory for a variable, array or object, and return a pointer to it.

    nullptr
        A canonical pointer value (i.e. a pointer which points to nothing). Useful for initialising pointers or checking if a pointer is valid.

    private
        Declare a class member which can only be accessed by functions within the class itself (i.e. not by functions outside the class which use an object of that class). Opposite of `public`.

    public
        Declare a class member which can be freely accessed by functions outside the class which use an object of that class. Opposite of `private`.

    this
        Pointer to the current object, which is passed implicitly to member functions. Useful for accessing other members of the same object if they have the same name as a local variable (e.g. a method argument).

    throw
        Throw an exception, which can be caught by a `catch` statement. (Similar to Python `raise`).

    true
        Boolean data indicating a true value. Opposite of `false`, and equivalent to `1`.

    virtual
        Declare a virtual function, which can be overridden by a function of the same name in a derived class. Indicates that the function should be called based on the type of the object, rather than the type of the pointer to the object.

    

