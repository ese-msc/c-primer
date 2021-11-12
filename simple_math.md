# Some Numerical Examples

Now that we've seen a C++ program at its most basic, let's look at some more useful examples. Again we're going to start from code you've already seen working in Python and convert it into C++

## A prime calculator

Let's start off with some Python code to list the prime numbers less than 1000.

_primes.py_
```python
    for i in range(2, 1000):
        j = 2
        flag = True
        while j**2<=i:
            if i%j == 0:
                flag = False
                break
            j += 1
        if flag:
            print(i)
```

```
_primes.cpp_
```c++
    #include <iostream>

    int main() {
        for (int i=2; i<1000; i++) {
            int j = 2;
            bool flag = true;
            while (j*j<i) {
                if (i%j) {
                    flag = false;
                    break;
                }
                j++;
            }
            if (flag) {
                std::cout << i << std::endl;
            }
        }
        return 1;
    }

```


## Programs with input

### Taking input from the keyboard



### Taking input straight from the command line


## Exercises

## Summary