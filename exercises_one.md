# Further Exercises

These additional exercises will allow you to test your new knowledge of C++ by asking you to translate more of your existing Python knowledge to your new language.

## A unit converter

Write a C++ program to take in an input in metres and return the distance in feet and/or inches. Remember that one inch is 2.54 cm, and that one foot is 12 inches.

## More means

Based on the code you've already seen to calculate the mean of a set of floating point numbers you read from the keyboard, try to update it to take in a list of integers. Watch out, you may find the final division a little trickier than you expected.

Here's the floating point means code again

```c++
#include <iostream>

int main(){
    int n;
    double a, sum=0;

    std::cout << "How many numbers would you like to enter?\n";
    std::cin >> n;

    for (int i=0; i<n; i++) {
        std::cout << "Enter number " << i+1 << std::endl ;
        std::cin >> a;
        sum += a;    
    }

    std::cout << "Mean is " << sum/n; 
    return 0;
}
```

## Implement a Gaussian

Write a C++ program to compute the Gaussian function

$$ f(x, m, s) = \frac{1}{s\sqrt{2\pi}}\exp\left(\left(-\frac{1}{2}\frac{x-m}{s}\right)^2\right) $$

You will probably want to use `#include <cmath>` at the top of your file to get the `exp` and `sqrt` functions. You might also want the `pow` function to implement the square (`pow(x, 3)` returns $x^3$). 

Your function can use fixed inputs, or read them in in any of the ways you now know.


