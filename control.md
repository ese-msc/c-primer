# C/C++ Control Structures

Control structures are what differentiate a computer program from a calculator, and allow us to repeat or avoid sections of code depending on the logical operation of the program. Many of the 

## Loops
```{index} Loops
```

### For loops
```{index} For loops
```


### While loops
```{index} While loops
```


### Do while
```{index} Do while loops
```


### Break and continue
```{index} break, continue
```


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

A form of condition which Python doesn't have an equivalent for is the `switch` statement. These start with `switch (`_expression_`)` and then have a block in following the form
```c++
switch (my_label) {
  case 1:
    
} 


## Exercise