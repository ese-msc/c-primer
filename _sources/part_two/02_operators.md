# C/C++ Operators
```{index} operators
```

## The Basic Operations
```{index} operators: basic
```

Like Python, C-like languages support the core mathematical operations on numerical data types, be they varables, or literals (i.e. symbols like `3` or `4.6754`). You can do any of the following:


|Operator| Operation |
|:------:|:---------:|
|   +    |  Addition |
|   -    | Subtraction|
|   *    | Multiplication|
|   /    | Division   |

Unlike Python there is no exponentiation operator (i.e. no `**`), which requires making a function call instead.

### Operations on mixed types
```{index} type conversion
```

Remember that in C++, the type of the result of an operation is determined by the types of the operands. If the operands are of different types, the compiler may automatically convert one of them to the type of the other. This is called _type conversion_ or _type casting_. For example, if you divide an integer by a floating point number, the integer will be converted to a float before the division is performed. Generally speaking, the compiler will try to convert the "smaller" type (the one with a smaller range or less precision) to the "larger" type, but you can also force the conversion by using a _type cast_.

One key difference from modern Python is that C++ does not automatically convert between integer and floating point types when performing division on integers with the `\` operator. This means that if you divide two integers, the result will be an integer, with any fractional part truncated. To get a floating point result, you must convert one of the operands to a floating point type first.

```c++

#include <iostream>


int main() {
    int a = 5;
    int b = 2;

    // This will print 2
    std::cout << a/b << std::endl;

    // This will print 2.5
    std::cout << (float)a/b << std::endl;

    return 0;
}
```

The code above demonstrates this behaviour, as well as the syntax for casting a variable to a different type . The `(float)` in the second `std::cout` statement is a _type cast_ which converts the integer `a` to a floating point number before the division is performed, refer back to the previous section for more information on type casting.

## Logical Operators
```{index} operators: logical
```

Again, as with Python, all the binary logical operators below work in C/C++

|Operator| Operation |
|:------:|:---------:|
|  `a == b`  |  equality test |
|  `a > b`   | greater than|
|  `a < b`   | less than|
|  `a >= b`  | greater than or equal to  |
|  `a <= b`  | less than or equal to  |
|  `!a`      | not |
|  `a !=  b` | not equal |
|  `a && b`  | and |
|  `a \|\| b`  | or |

In C++ these functions return a `bool` data type which can be equal to `true` or `false` (note the capitalization differs from Python). However, thanks to an implicit type conversion rule, _all_ positive integers evaluate to true and the value zero evaluates to false. As in Python, using comparisons with floating point numbers can be tricky due to the way they are stored in memory, and you should be careful when using them to test for equality.

## Other Useful Operators
```{index} operators: other
```

|Operator| Operation |
|:------:|:---------:|
| `a++`  | increment |
| `a--`  | decrement |
| `a += b`  | increment by `b`|
| `a -= b`  | decrement by `b`|
| `a % b`  | remainder |
| `a << 2`  | bitwise left shift |
| `a >> 2`  | bitwise right shift |

## Operators For Completionists
```{index} operators: advanced
```

|Operator| Operation |
|:------:|:---------:|
| `&`  | bitwise and |
| `\|`  | bitwise or |
| `^`  | bitwise xor |
| `~`  | bitwise not |
| `?`  | conditional ternary operator |

## The Order of Evaluation
```{index} evaluation order
```

There is a well defined default order of evaluation for operators in C/C++ which is worth knowing. The order of evaluation for commonly used operations is:

1. `()` parentheses
2. `++` and `--` increment and decrement
3. `*` and `/` multiplication and division
4. `+` and `-` addition and subtraction
5. `<<` and `>>` bitwise left and right shift
6. `==`, `!=`, `>`, `<`, `>=`, `<=` comparison
7. `!` not
8. `&&` and `||` logical and and or
9. `=`, `+=`, etc. (i.e assignment)

## Summary

We've now revised the basic operations which C++ allows us to apply to values in expressions, most of which have a Python equivalent. In the next section, we will look in more detail at the various control structures C++ supplies to organise, repeat or skip sections of code within a function.

