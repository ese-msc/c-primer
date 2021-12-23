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