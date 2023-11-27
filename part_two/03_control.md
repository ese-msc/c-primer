# C/C++ Control Structures

Control structures are what differentiate a computer program from a calculator, and allow us to repeat or avoid sections of code depending on the logical operation of the program. Many of the fundamental details are very similar to Python, and generally sections will translate fairly easily, although not perfectly, between the two languages.

## Loops
```{index} Loops
```

### For loops
```{index} For loops
```

Probably the most common type of loop in C/C++ (particularly in numerical codes and scientific computation) is the `for` loop. While this has a different syntax than Python, the core idea is the same. A very basic loop might look like

```c++
for (int i=0; i<10; i++) {
    std::cout << i;
}
```
You'll note that the actual `for` clause is split into three statements (separated by `;` tokens).

 The first statement_initializes_ our counting mechanism, e.g. (as in this case, `int i=0`) declaring a counter variable and pointing it to its first value. In theory we could do multiple things in here (e.g. reset multiple existing variables, just call a function etc.) but in practice we're likely just to set up one counting variable.

 The second statement sets the termination or halting criterion. The `for` loop statement will executive each time as long as the statement here (in our case `i<10`) evaluates true. As soon as that is no longer the case, the loop stops and execution carries on down the function.

 The third statement (in this case `i++`) specifies increment or decrement for the loop, and is applied each time that the loop is gone around. We use the `++` increment operator (which does the same thing as `i=i+1`) so our loop will runs 10 times, with `i` taking the values 0 to 9. If we used a different statement (e.g. `i+=2`) we could change the effective "stride" of the loop.

### While loops
```{index} While loops
```

As with Python, C++ has `while` loops which just test a termination statement, and continues to execute the loop block so long as it is true. As an example, lets write [Newton Rapheson]() square root finder in Python and C++:

_for Python_
```python
def my_sqrt(y):
    x=0
    while (x*x-y)*(x*x-y)>1.0e-6:
        x = (x + y / x) / 2
```

_for C++_
```c++
double my_sqrt(double y){
    double x=0.0;
    while ((x*x-y)*(x*x-y)>1.0e-8){
        x = (x+y/x)/2;
    }
    return x;
}
```

### Do while
```{index} Do while loops
```

A form of logic Python doesn't have is the `do ... while` loop. This again tests a statement to decide whether to continue execution, but the test now comes _after_ the loop block, which is thus guaranteed to execute once. This can be useful if the block initialises something which should then be checked:

```c++
int n;
do {
    std::cout >> "Enter a number larger than 100.\n";
    std::cin >> n;
} while (n <= 100>); // note the ; here
```

### Break continue and exit
```{index} break, continue
```

The `break` and `continue` statements are used inside loops to skip either all remaining iterations (for `break`) or the next iteration (for `continue`). These statements behave just like their Python equivalents, in that they only apply to the innermost loop of the function currently being executed, and can't be used outside of a loop structure. To quit the entire program at once, you should use the `exit(1)` function, supplying an integer return value (remember, a zero return value is usually taken to mean things went ok, and an other value that something went ) 


## Conditionals


### If, else if, and else

As with Python, C-like languages use if statements to conditionally process blocks of code. However, the C syntax is once again a little different.

Where a PEP8 compliant Python conditional might look like

```python
    my_age = 70
    your_age = input()

    if my_age < your_age:
        print("Ha! I'm younger than you!")
    elif my_age > your_age:
        print("Ha! I'm older than you!")
    else:
        print("Ha! We're the same age!")
```
a C++ equivalent main program might look like
```c++
   #include <iostream>

   int main() {
       int my_age=70, your_age;
       std:cin >> your_age;
    if (my_age < your_age) {
        std::cout <<"Ha! I'm younger than you!\n";
    } else if (my_age > your_age) {
        std::cout << "Ha! I'm older than you!";
    } else {
        print("Ha! We're the same age!")
    }

```

The key differences are:
  - The `()` brackets are required around the expression being tested.
  - There is no `elif` keyword, instead we use `else if`.

Note that the `{}` brackets are only strictly necessary if there is more than one statement in the conditional statement block. We could always choose to write:
    ```c++
    if (my_age < your_age) std::cout <<"Ha! I'm younger than you!\n";
    else if (my_age > your_age) std::cout << "Ha! I'm older than you!";
    else print("Ha! We're the same age!")
    ```
However, the version with brackets is more explicit and makes it harder to get confused about which statements are actually conditional.


### The switch statement

A form of condition which was only recently introduced in Python  is the `switch` statement, which corresponds to the Python `match`statement. In C++ these start with `switch (`_expression_`)` and then have a block in following the form
```c++
switch (my_label) {
  case 1:
    my_cool_function_one(); 
    break;
  case 2:
    my_cool_function_two();
    break;
  case 3:
    my_cool_function_one();
    my_cool_function_two();
    break;
  case default:
    my_cool_function_three();
} 
```

In the apove example the code will choose which functions to call depending on if `my_label` is 1,2,3 or something else. Note that without the `break` statements execution will "fall through" from `case` statement blocks at the top down to the ones at the bottom, which in this example would mean `my_cool_function_one` and `my_cool_function_two` being called twice. This is slightly different to the Python `match` statement, which will only execute the first matching case.

## Summary

We've now had a brief look at many of the ways you can control the logical flow of a C++ program, and seen that many of them are similar to the patterns you know from Python. In the next section we will take a deeper look at functions specifically, including their syntax, how to call them and ways they are used.