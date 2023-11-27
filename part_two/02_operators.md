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

Unlike Python there is no exponentiation operator (i.e. no `**`), which requires a function call instead.

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
|  `a <= b` | less than or equal to  |
!  `!a`     | not |
| `a !=  b` | not equal |
|  `a && b` | and |
| `a || b`  | or |

In C++ these functions return a `bool` data type which can be equal to `true` or `false` (note the capitalization differs from Python). However, thanks to an implicit type conversion rule, _all_ positive integeres evaluate to true and the value zero evaluates to false. 

## Other Useful Operators
```{index} operators: other
```

|Operator| Operation |
| `a++`  | increment |
| `a--`  | decrement |
| `a % b`  | remainder |
| `a << 2`  | bitwise left shift |
| `a >> 2`  | bitwise right shift |

## Operators For Completionists
```{index} operators: advanced
```

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

