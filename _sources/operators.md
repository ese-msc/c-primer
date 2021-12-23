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
| `and` b/ `a & b` | and |
| or  / `a | b`  | or |

In C++ these functions return a `bool` data type which can be equal to `true` or `false`. However, thanks to an implicit type conversion rule, _all_ positive integeres evaluate to true and zero evaluates to false. 

## Other Useful Operators
```{index} operators: other
```

## Operators For Completionists
```{index} operators: advanced
```

## The Order of Evaluation
```{index} evaluation order
```

## Summary

We've now revised the basic operations which C++ allows us to apply to values in expressions, most of which have a Python equivalent. In the next section, we will look in more detail at the various control structures C++ supplies to organise, repeat or skip sections of code within a function.

