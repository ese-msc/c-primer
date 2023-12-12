# Some Numerical Examples

Now that we've seen a C++ program at its most basic, let's look at some more useful examples. Again we're going to start from code you've probably already seen working in Python and convert it into C++ instead.

## A prime calculator

Let's start off with some Python code to list the prime numbers less than 1000.

_primes.py_
```python
    # A simple primes calculator
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

Now let's convert it into a C++ version

_primes.cpp_
```c++
    // A simple primes calculator
    #include <iostream>

    int main() {
        for (int i=2; i<1000; i++) {
            int j = 2;
            bool flag = true;
            while (j*j<=i) {
                if (i%j==0) {
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

Once again we need to include the `iostream` header (to be able to write to the screen) and to place our code inside a `main` function so that it runs when our program is started. The other big difference is that our variables need to be declared to have particular datatypes (e.g. `int j`) at or before their first point of use. This is important, and the code will not compile without it, since the C++ compiler uses the type information to work out which versions of functions to call and to make sure that users have not made mistakes.

Note that we've also included a comment in our code. In C/C++ one-line comments start with `//`. We can also write an entire comment block:

``` c++ 
/* This text will be ignored by a compiler.
And so will this!
To end the comment we need a */

int main(){
    a = 1;
    a--;
    return a;
}
```

## The forward Euler method

Let's now look at a more complicated example, the forward Euler method for solving a simple ODE. We'll start with the Python code:

_forward_euler.py_
```python
    # A simple forward Euler solver for the ODE dy/dt = -y
    import numpy as np
    import matplotlib.pyplot as plt

    def f(y):
        return -y

    y0 = 1
    t0 = 0
    t1 = 10
    h = 0.1

    t = np.arange(t0, t1+h, h)
    y = np.zeros_like(t)
    y[0] = y0

    for i in range(1, len(t)):
        y[i] = y[i-1] + h*f(y[i-1])

    plt.plot(t, y)
    plt.show()
```

Now let's convert it into a C++ version

```c++

#include <iostream>

double f(double y) {
    return -y;
}

int main(void){

    const int nsteps = 100;
    double y0 = 1;
    double t0 = 0;
    double t1 = 10;
    double h = t1/nsteps;

    double t[nsteps+1];
    double y[nsteps+1];

    t[0] = t0;
    y[0] = y0;

    for (int i=1; i<=nsteps; i++) {
        t[i] = t[i-1] + h;
        y[i] = y[i-1] + h*f(y[i-1]);
    }

    for (int i=0; i<n; i++) {
        std::cout << t[i] << " " << y[i] << std::endl;
    }

    return 0;
}

```

Note that unlike in Python, plotting in C++ is hard work, so we're just printing the values to screen instead.

## Quadrature

Now we'll implement two quadrature methods, the midpoint and the trapezium rules. We'll start with the Python code (see the Computational Mathematics course for the annotated versions):

```python

import numpy as np

def midpoint_rule(a, b, func, number_intervals=10):
    interval_size = (b - a)/number_intervals

    I_M = 0.0
    mid = a + (interval_size/2.0)

    while (mid < b):
        I_M += interval_size * func(mid)
        mid += interval_size
    return I_M

def trapezium_rule(a, b, func, number_intervals=10):
    interval_size = (b - a)/number_intervals

    I_T = 0.0
    x = a + interval_size

    while (x < b):
        I_T += interval_size * (func(x) + func(x - interval_size))/2.0
        x += interval_size
    return I_T

def f(x):
    return np.sin(x)

print(midpoint_rule(0, np.pi, f))
print(trapezium_rule(0, np.pi, f))
```

Now let's convert it into a C++ version

```c++
#include <iostream>
#include <cmath>

double midpoint_rule(double a, double b, double (*func)(double), int number_intervals=10) {
    double interval_size = (b - a)/number_intervals;

    double I_M = 0.0;
    double mid = a + (interval_size/2.0);

    while (mid < b) {
        I_M += interval_size * func(mid);
        mid += interval_size;
    }
    return I_M;
}

double trapezium_rule(double a, double b, double (*func)(double), int number_intervals=10) {

    double interval_size = (b - a)/number_intervals;

    double I_T = 0.0;
    double x = a + interval_size;

    while (x < b) {
        I_T += interval_size * (func(x) + func(x - interval_size))/2.0;
        x += interval_size;
    }
    return I_T;
}

double f(double x) {
    return std::sin(x);
}

int main(void) {
    std::cout << midpoint_rule(0, M_PI, f) << std::endl;
    std::cout << trapezium_rule(0, M_PI, f) << std::endl;
    return 0;
}
```

Note that we've had to include the `cmath` header to get access to the `sin` function. We've also had to declare the function `f` as taking a double and returning a double, and then pass it as an argument to the quadrature functions. This is because C++ doesn't have a built-in `sin` function, but instead has a `sin` function for each of the floating point types (e.g. `float`, `double`, `long double`), and the compiler needs to know which one we want to use.

The declaration and use of function pointers in the C++ versions of the `midpoint_rule` and `trapezium_rule` is more complicated than the Python version, but it's not too bad once you get used to it. We'll talk more about this in a later section.

## Exercises

1. Try to modify the C++ primes code to calulate the first 100 prime numbers instead.
2. Try to write a C++ version of the backwards Euler method for the same ODE.
3. Try to write a C++ version of the Simpson's rule quadrature method, and include it in the quadrature example.

## Summary

We've now seen C++ used to solve some simple numerical problems of the sort which you're already used to solving with Python. In the next section we'll look at some ways of modifying the behaviour of our code at runtime based on user input.