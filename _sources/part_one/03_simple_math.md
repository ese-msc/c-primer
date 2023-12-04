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

## Programs with input

### Taking input from the keyboard

The counterpart to `std::cout` is `std::cin`. It's usage is similar but "in the other direction". For example:

```c++
#include <iostream>

int main(){

    char name[256];

    std::cout << "What's your name?\n";
    std::cin >> name;
    std::cout << "Hello " << name << "!\n";

    return 0;
}
```

```{note} 
To run this using Docker plus VS code, you will need to run the compile command in full in the terminal:
    ```
    g++ hello2.cpp -o hello2
    ```
```

The `>>` operator will automatically convert the input into an appropriate form for the datatype (as long as it's one of the defaults). In the example above, this is just to a string, but we can also convert to integers or floating point numbers. Let's have an example, for example a program to calculate the mean of a sequence of floating point numbers.

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

### Taking input straight from the command line

As we saw with Python, another useful way to pass information into a program is on the command line. So far we have always used `main` functions with no input, but a longer form of the input signature is

```
int main(int argc, char* argv[])
```

Here we have two variables which are automatically assigned by the operating system, the integer `argc`, and an array of strings, `argv`. Just like with the Python `sys.argv`, the array is populated with a space separated list of the command line arguments used to call the program, with the first entry (`argv[0]`) equal to the name used to set the program running.

```c++
#include <iostream>

int main(int argc, char* argv[]){
    double a, sum=0;

    for (int i=1; i<argc; i++) {
        a =  std::atof(argv[i]);
        sum += a;    
    }

    std::cout << "Mean is " << sum/(argc-1) <<std::endl; 
    return 0;
}
```

### Taking input from files

The last useful way we'll talk about to pass information in to a program is via a file. This is more involved than the previous versions, so don't be too worried if you don't follow all the details.

As with input/output the standard methods differ somewhat between C & C++. In C we use a collection of functions from `stdio.h`. For example to write a file:

```c
#include <stdio.h>

int main()
{
   FILE *fptr;

   fptr = fopen("example.txt","w"); // A lot like the Python open function

   if(fptr == NULL) // We have to do our own error checks
   {
      printf("Error!");   
      exit(1);             
   }

   fprintf(fptr,"%d",  1000); // Write a number
   fclose(fptr);

   return 0;
}

```
to read a file we'd use
```c
   int num;
   fptr = fopen("example.txt","r"); 
   fscanf(fptr,"%d", &num);
```
instead. We'll explain the use of `*` and `&` in the code above in Part III.

For C++ we can treat files like we do the screen by treating them as _streams_ and reading or writing with the `<<` and `>>` operators. So to write ouput

```c++
#include <fstream>

int main () {

  std::fstream fs;
  fs.open ("example.txt", std::fstream::out);
  
  fs << 1000; // write 1000 to example.txt
  fs.close();

  return 0;
}
```

or
```c++
  int num;
  fs.open ("example.txt", std::fstream::in);
  /* read an int from example.txt (which is assumed)
  to exist already. Unlike Python, we need to write 
  additional code if that might not be true.*/
  fs >> num; 
  fs.close();
```
to read from the file instead.

## Exercises

1. Try to modify the C++ primes code to calulate the first 100 prime numbers instead. 
2. Next, add the code to take input from the keyboard on how many numbers to calculate.
3. Next, write a version which takes the number of primes to calculate as input from the command line (you may need the `std::atoi` function).
4. Finally, update your code to write the prime numbers to a file, taking the name of the file as input.

## Summary

We've now seen C++ used to solve some simple numerical problems of the sort which you're already used to solving with Python. In the next section we'll look in detail at some of the things that can go wrong while trying to compile C/C++ code, how to understand the error messages which are presented, and what we can do to attempt to fix the problems.