========
Keywords
========

C Keywords
##########

Storage keywords
================

.. glossary::

    auto
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
        Exit a function and pass any `return` value to the calling routine. 
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

    auto
        Declare a variable which automatically identifies its data type based on the context in which it is used. *Different from C behaviour*.
    bool
        Boolean datatype.
    catch
        Associate exception handlers with a `try` statement block, somewhat similar to Python.
    class
        Object oriented combined structure holding both data and functions, which usually act upon that data.
    delete
    false
        Boolean data indicating a false value.
    friend
        Specifier indicating a function/class can access private or protected data stored in the declaring class.
    operator
        Declares an overloading of an operator for a user declared data type (i.e. lets the programmer use it with standard C++ operators such as `+` or `<<`).
    namespace
    new
    private
    public
    this
    throw
    true
    virtual

    

