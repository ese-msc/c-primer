# Further Exercises

## Fizzbuzz in C++

Try to convert the following "Fizzbuzz" program into C++:

```python
print("How many numbers should I run to?")
n = input()
for i in range(1, n+1):
    if i%15==0:
        print("Fizzbuzz\n")
    elif i%3==0:
        print("Fizz\n")
    elif i%5==0:
        print("Buzz\n")
    else:
        print(i)
```

you will need a loop (probably a `for()` loop) as well an `if` block.

## Reversing a number

The following Python program reverses a number:

```python
print("Enter a number")

def nreverse(n):
    rev = 0
    while n>0:
        rev = rev*10 + n%10
        n = n//10
    return rev

n = input()

print("The reversed number is", nreverse(n))
```

Try to convert this program into C++.

## Greatest Common Divisor

Write a C++ program to find the greatest common divisor of two numbers. The greatest common divisor of two numbers is the largest number that divides both of them.

You can use the following algorithm:

1. If `a` is greater than `b`, swap `a` and `b`.
2. Divide `b` by `a` and assign the remainder to `r`.
3. If `r` is 0, then the GCD is `a`, STOP.
4. Assign `a` the value of `b` and `b` the value of `r`.
5. Go to step 2.

This algorithm is known as the Euclidean algorithm. It works because the GCD of two numbers also divides their difference. So, if `a` is the GCD of `b` and `c`, then `a` is also the GCD of `b` and `b-c`. Since `r` is smaller than `a`, the algorithm will eventually reach a point where `r` is 0, so it is guaranteed to terminate.



