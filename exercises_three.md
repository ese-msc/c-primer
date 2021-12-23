# Further Exercises

## Swapping two objects

In Python it is very easy to write some code to swap two object values between two names

```python
a, b = b, a
```

In C and C++ this is more complicated, and the most understandable way to do it requires writing a function.

Try to do this three different ways (these are written in approximate order of difficulty):
1. Write a function to swap the values of two different scalar `int` values. This will need to be "pass by reference", either directly, or using pointers, as well as a temporary variable.
2. Write a function to swap the values referenced by two `*int` pointers by changing the values. If you went the pointer version for 1. this is basically the same code.
3. Write a function to swap the values referenced two `*int` pointers by changing the targets. This can be done in a similar way, but adds an additional layer of indirection. Ask yourself, do you want to pass by reference, or by value?
